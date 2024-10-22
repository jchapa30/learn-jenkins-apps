pipeline {
    agent any

    stages {
        stage('Test Docker') {
            steps {
                script {
                    // Check the Docker version
                    sh 'docker version'
                    sh 'ls -la'
                }
            }
        }

        stage('Non-Docker Step') {
            steps {
                script {
                    // An example command that doesn't use Docker
                    sh 'echo "This is a non-Docker step in the pipeline."'
                    sh 'ls -la'
                }
            }
        }
    }
}