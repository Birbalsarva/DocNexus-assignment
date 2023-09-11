pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Test') {
            steps {
                // Copy your files to the destination directory
                sh "cp -r * /var/www/html/"
            }
        }
        stage('Deploy to AWS EC2') {
            steps {
                script {
                    def remote = [:]
                    remote.name = 'YourSSHKeyName'  // Use the SSH credential ID you configured in Jenkins
                    remote.host = '54.206.111.36'  // Your EC2 instance public IP address
                    remote.user = 'ubuntu'  // SSH username (for Ubuntu instances)
                    remote.allowAnyHosts = true
                    remote.identityFile = '/home/ubuntu/ssh_key/Bs.key'  // Path to your private key

                    remote.command = """
                        # Navigate to the directory containing your website files
                        cd /var/www/html

                        # Copy your website files to the remote server
                        cp -r * ${remote.user}@${remote.host}:/var/www/html/
                    """
                    sshCommand remote: remote, failOnError: true
                }
            }
        }
    }
}
