pipeline {
    agent any

    environment {
        SSH_CRED = 'jenkins-key'
        SERVER_IP = '3.84.128.235'
        REMOTE_USER = 'ubuntu'
        WEB_DIR = '/var/www/html/'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/abhigiri07/static-website-project.git', branch: 'main'
            }
        }

        stage('Deploy to Apache Server') {
            steps {
                sshagent(credentials: ["${SSH_CRED}"]) {
                    sh '''
                        echo "Cleaning old files on server..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "sudo rm -rf ${WEB_DIR}/*"

                        echo "Uploading project files to /tmp..."
                        scp -r * ${REMOTE_USER}@${SERVER_IP}:/tmp/static-website

                        echo "Verifying /tmp content..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "ls -l /tmp"

                        echo "Deploying to Apache directory..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "sudo cp -r /tmp/static-website/* ${WEB_DIR}/"

                        echo "Restarting Apache to clear cache..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "sudo systemctl restart apache2"

                        echo "✅ Deployment completed!"
                    '''
                }
            }
        }
    }
}
