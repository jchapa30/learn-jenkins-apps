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
    }
}
