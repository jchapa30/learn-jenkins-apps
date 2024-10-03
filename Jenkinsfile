pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }

        stage('Initial Check') {
            steps {
                // Print the node and npm versions
                sh 'node --version'
                sh 'npm --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Clean npm cache and install dependencies
                sh 'npm cache clean --force'
                sh 'npm ci' // or use 'npm install' if you prefer
            }
        }

        stage('Run Tests') {
            steps {
                // Add your testing command here, for example:
                sh 'npm test'
            }
        }

        // Add more stages as needed
    }

    post {
        always {
            // Archive the artifacts or perform cleanup actions
            archiveArtifacts artifacts: '**/build/**', fingerprint: true
            cleanWs() // Clean workspace
        }
    }
}

