pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: 'd5cc2ef1-b72c-460a-9455-b24e177e1993', url: 'https://github.com/shan376/pro35.git'
            }
        }

        stage('Setup SSH Known Hosts') {
            steps {
                sh '''
                mkdir -p ~/.ssh
                chmod 700 ~/.ssh
                ssh-keyscan -H 13.59.46.192 >> ~/.ssh/known_hosts
                chmod 644 ~/.ssh/known_hosts
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                ansible-playbook -i inventory playbook.yml
                '''
            }
        }
    }

    post {
        failure {
            echo '❌ Pipeline failed. Check logs for details.'
        }
        success {
            echo '✅ Pipeline completed successfully!'
        }
    }
}
