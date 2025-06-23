pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/shan376/pro35.git',
                        credentialsId: 'd5cc2ef1-b72c-460a-9455-b24e177e1993'
                    ]]
                ])
            }
        }

        stage('Run Ansible') {
            steps {
                withEnv(["ANSIBLE_HOST_KEY_CHECKING=False"]) {
                    sh '''
                    mkdir -p ~/.ssh
                    chmod 700 ~/.ssh
                    ssh-keyscan -H 13.59.46.192 >> ~/.ssh/known_hosts
                    ansible-playbook -i inventory.ini playbook.yml
                    '''
                }
            }
        }
    }
}
