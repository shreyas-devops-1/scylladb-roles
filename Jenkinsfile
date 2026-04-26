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

        stage('Verify Repository Files') {
            steps {
                sh '''
                    echo "===== Repository Files ====="
                    ls -la

                    echo "===== Roles Directory ====="
                    ls -la roles/

                    echo "===== Ansible Version ====="
                    ansible --version
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                    echo "===== Running Ansible Playbook ====="
                    sudo ansible-playbook -i ${INVENTORY} ${PLAYBOOK}
                '''
            }
        }
    }

    post {
        success {
            echo 'ScyllaDB deployment completed successfully.'
        }

        failure {
            echo 'Pipeline failed. Please check Jenkins console output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}