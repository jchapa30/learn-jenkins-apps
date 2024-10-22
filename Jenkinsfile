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
                // Any commands you want to run outside the Docker container go here
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
    }
}
