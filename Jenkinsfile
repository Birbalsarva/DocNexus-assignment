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
                // Add your build and test steps here
                // For example, if you are building a static website, you might just copy the files.
                sh "cp -r my_website/* /var/www/html/"
            }
        }
        stage('Deploy to AWS EC2') {
            steps {
                script {
                    def remote = [:]
                    remote.name = 'YourSSHKeyName'  // Use the SSH credential ID you configured in Jenkins
                    remote.host = '54.206.111.36'  // Your EC2 instance public IP address
                    remote.user = 'deploy-user'  // SSH username on your EC2 instance
                    remote.allowAnyHosts = true
                    remote.identityFile = '/home/ubuntu/ssh_key/Bs.key'  // Path to your private key

                    remote.command = """
                        # Navigate to the directory containing your website files on the remote server
                        cd /var/www/html

                        # Copy your 'my_website' directory from the workspace to the remote server
                        cp -r ${WORKSPACE}/my_website/* .
                    """
                    sshCommand remote: remote, failOnError: true
                }
            }
        }
    }
}
