pipeline { 
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'ls -la'
                sh 'node --version'
                sh 'npm --version'
                sh 'npm ci'
                sh 'npm run build'
                sh 'ls -la'
            }
        }

        stage('Non-Docker Step') {
            steps {
                sh 'echo "This is a non-Docker step."'
                sh 'ls -la'
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'echo "Checking for the presence of index.html"'
                sh 'test -f build/index.html && echo "index.html exists" || echo "index.html does not exist"'
                sh 'npm test'
                sh 'node --version'
                sh 'npm --version'
                sh 'npm ci'
            }
        }

        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.48.1-noble'
                    reuseNode true
                    args '-u root:root'
                }
            }
            steps {
                sh 'echo "Installing serve package globally for E2E testing"'
                sh 'npm install -g serve'
                
                // Start the server in the background on a specific port, capturing PID to kill it later
                sh 'serve -s build -l 5000 & echo $! > serve.pid'

                // Wait a moment to allow the server to start
                sh 'sleep 5'
                
                // Run Playwright tests against the local server on port 5000
                sh 'npx playwright test --base-url=http://localhost:5000'

                // Kill the serve process to ensure clean-up
                sh 'kill $(cat serve.pid)'
            }
        }
    }
    
    post {
        always {
            // Cleanup any leftover processes if E2E stage fails to clean up
            sh 'if [ -f serve.pid ]; then kill $(cat serve.pid) || true; fi'
            sh 'rm -f serve.pid'
        }
    }
}
