
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
                    remote.host = 'your-ec2-instance-ip'
                    remote.user = 'ec2-user' // Replace with your EC2 SSH user
                    remote.identityFile = '/path/to/your/aws/key.pem' // Replace with your AWS private key path

                    // Clone your GitHub repository on the EC2 instance
                    remote.command = """
                        cd /path/to/deployment
                        git clone https://github.com/Birbalsarva/DocNexus-assignment.git
                    """

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
