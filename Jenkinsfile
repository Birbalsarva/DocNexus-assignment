pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository
                script {
                    git 'https://github.com/Birbalsarva/DocNexus-assignment.git'
                }
            }
        }
        
        stage('Build') {
            steps {
                // Build your web application (if needed)
                echo 'Building static HTML file...'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests (if needed)
                sh 'npm install htmlhint'
                sh 'node_modules/.bin/htmlhint index.html'
            }
        }
        
        stage('Deploy to AWS EC2') {
            steps {
                // Use SSH to copy the files to your EC2 instance
                script {
                    sshagent(['Bs.key']) {
                        sh 'scp -i /home/ubuntu/ssh_key/Bs.key -o StrictHostKeyChecking=no index.html ubuntu@54.206.111.36:/path/to/destination'
                    }
                }
            }
        }
    }
}

