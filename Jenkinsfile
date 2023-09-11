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
                // No build step needed for a static HTML file
            }
        }

        stage('Test') {
            steps {
                // Install HTMLHint (you may need to adjust this based on your environment)
                sh 'npm install -g htmlhint'
                
                // Run HTMLHint to validate the HTML file
                sh 'htmlhint index.html'
            }
        }

        stage('Deploy to AWS EC2') {
            steps {
                // Use SSH to connect to your AWS EC2 instance and clone your GitHub repo
                script {
                    def remote = [:]
                    remote.name = 'AWS_EC2'
                    remote.host = '54.206.111.36' // Replace with your EC2 instance's public IP
                    remote.user = 'ubuntu' // Set the SSH user for your EC2 instance
                    remote.identityFile = '/home/ubuntu/ssh.key/Bs.key' // Set the path to your AWS private key

                    // Clone your GitHub repository into the Jenkins workspace
                    remote.command = "git clone https://github.com/Birbalsarva/DocNexus-assignment.git"

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
