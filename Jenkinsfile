pipeline {
    agent any

    stages {

        stage('Pull Latest Code') {
            steps {
                git branch: 'main', url: 'https://github.com/abhigiri07/static-website-project.git'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ubuntu@<EC2_PUBLIC_IP> "
                            sudo rm -rf /var/www/html/static-website-project/*
                            sudo git clone https://github.com/abhigiri07/static-website-project.git /var/www/html/static-website-project
                            sudo chown -R www-data:www-data /var/www/html/static-website-project
                            sudo chmod -R 755 /var/www/html/static-website-project
                            sudo systemctl restart apache2
                        "
                    '''
                }
            }
        }
    }
}
