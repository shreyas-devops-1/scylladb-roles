pipeline {
    agent any

    environment {
        GIT_REPO  = 'https://github.com/shreyas-devops-1/scylladb-roles.git'
        BRANCH    = 'main'
        PLAYBOOK  = 'playbook.yml'
        INVENTORY = 'inventory.ini'
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                    sudo ansible-playbook -i ${INVENTORY} ${PLAYBOOK}
                '''
            }
        }
    }
}