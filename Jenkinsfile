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
                }
            }
            steps {
                sh 'echo "Installing serve package globally for E2E testing"'
                sh 'npm install -g serve'
                sh 'serve -s build &'
                sh 'npx playwright test'
            }
        }
    }
}
