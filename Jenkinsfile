pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
            }
        }
        
        stage('Build') {
            steps {
                // No build step needed for a static website
            }
        }

        stage('Deploy to Server') {
            steps {
                // Use SSH to copy website files to the server
                sh '''
                    ssh user@your-server 'mkdir -p /path/to/deployment'
                    scp -r website/* user@your-server:/path/to/deployment/
                '''
            }
        }
    }

    post {
        success {
            // Perform any post-deployment actions or notifications on success
            echo 'Deployment successful!'
        }
        failure {
            // Handle failure scenarios
            echo 'Deployment failed!'
        }
    }
}
