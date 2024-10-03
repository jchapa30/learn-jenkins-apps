pipeline {
    agent any

    stages {
        stage('Without Docker') {
            steps {
                script {
                    sh 'echo "This stage runs without Docker"'
                }
            }
        }
        stage('With Docker - Node 18 Alpine') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            steps {
                script {
                    sh 'echo "This stage runs inside a Docker container (Node 18 Alpine)"'
                }
            }
        }
    }
}

