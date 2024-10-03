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

        stage('Build') {
            steps {
                // Build command (replace this with your actual build command)
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                script {
                    // Print message for Test stage
                    echo 'Test stage'

                    // Check if index.html exists in the build directory
                    sh '''
                    if [ -f ./build/index.html ]; then
                        echo "index.html exists in the build directory."
                    else
                        echo "index.html does not exist in the build directory."
                        exit 1
                    fi
                    '''

                    // Run unit tests
                    sh 'npm test'
                }
            }
        }
    }

    post {
        always {
            // Archive the artifacts or perform cleanup actions
            archiveArtifacts artifacts: '**/build/**', fingerprint: true
            cleanWs() // Clean workspace
        }
        success {
            echo "Build and tests successful!"
        }
        failure {
            echo "Build or tests failed!"
        }
        // Publish the JUnit test results
        always {
            junit 'test-results/junit.xml'
        }
    }
}


