pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                 git url: "https://github.com/Birbalsarva/DocNexus-assignment.git", branch: "main"
            }
        }
        stage('Build and Test') {
            steps {
                sh "cp -r * /var/www/html/"
            }
        }
        stage('Deploy to AWS EC2') {
            steps {
                script {
                    def remote = [:]
                    remote.name = 'YourSSHKeyName'  
                    remote.host = '54.206.111.36'  
                    remote.user = 'ubuntu'  
                    remote.allowAnyHosts = true
                    remote.identityFile = '/home/ubuntu/ssh_key/Bs.key' 

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
