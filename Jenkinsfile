pipeline { 
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true // Reuse the same container for the pipeline stages
        }
    }
    stages {
        stage('Initial Check') {
            steps {
                // List all files in the workspace
                sh 'ls -al'
                
                // List Node.js and npm versions
                sh 'node --version'
                sh 'npm --version'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install dependencies using npm ci
                sh 'npm ci'
            }
        }
        stage('Run Build') {
            steps {
                // Run the build command
                sh 'npm run build'
            }
        }
        stage('Final Check') {
            steps {
                // List all files in the workspace again
                sh 'ls -al'
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}

