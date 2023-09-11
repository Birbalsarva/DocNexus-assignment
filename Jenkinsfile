pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                git branch: 'main', url: 'https://github.com/Birbalsarva/DocNexus-assignment.git'
            }
        }

        stage('Build') {
            steps {
                // No build step needed for a static HTML file, so we'll just echo a message
                echo 'Building static HTML file...'
            }
        }

        stage('Test') {
            steps {
                // Install HTMLHint locally in the workspace
                sh 'npm install htmlhint'
                
                // Run HTMLHint to validate the HTML file
                sh 'node_modules/.bin/htmlhint index.html'
            }
        }

        stage('Deploy to AWS EC2') {
            steps {
                script {
                    def remote = [:]
                    remote.name = 'AWS_EC2'
                    remote.host = '54.206.111.36' // Replace with your EC2 instance's public IP
                    remote.user = 'ubuntu' // Set the SSH user for your EC2 instance
                    remote.identityFile = '/home/ubuntu/ssh.key/Bs.key' // Set the path to your AWS private key

                    // Copy your static website files to the EC2 instance
                    remote.command = "scp -i ${remote.identityFile} -r * ${remote.user}@${remote.host}:/path/to/destination/folder"
                    
                    sshCommand remote: remote
                }
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
