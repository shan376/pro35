pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/shan376/pro35.git',
                        credentialsId: 'your-git-credentials-id'
                    ]]
                ])
            }
        }

        stage('Run Ansible') {
            steps {
                withEnv(["ANSIBLE_HOST_KEY_CHECKING=False"]) {
                    sh '''
                    mkdir -p /var/lib/jenkins/.ssh
                    chmod 700 /var/lib/jenkins/.ssh
                    ssh-keyscan -H 13.59.46.192 >> /var/lib/jenkins/.ssh/known_hosts
                    ansible-playbook -i inventory.ini playbook.yml
                    '''
                }
            }
        }
    }
}
