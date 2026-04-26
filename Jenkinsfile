pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/shreyas-devops-1/scylladb-roles.git'
        BRANCH = 'main'
        PLAYBOOK = 'playbook.yml'
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

        stage('Verify Files') {
            steps {
                sh '''
                    echo "Checking repository files..."
                    ls -la
                    echo "Checking Ansible version..."
                    ansible --version
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh """
                    ansible-playbook -i ${INVENTORY} ${PLAYBOOK}
                """
            }
        }
    }

    post {
        success {
            echo 'ScyllaDB deployment completed successfully.'
        }

        failure {
            echo 'Pipeline failed. Please check logs.'
        }
    }
}
