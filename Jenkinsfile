pipeline {
    agent any

    environment {
        TF_DIR = './'
        ANSIBLE_DIR = './'
    }

    stages {
        stage('Terraform Init & Apply') {
            steps {
                dir("${TF_DIR}") {
                    sh 'terraform init'
                    sh 'terraform apply -auto-approve'
                }
            }
        }

        stage('Ansible Provisioning') {
            steps {
                dir("${ANSIBLE_DIR}") {
                    sh 'ansible-playbook -i inventory setup.yml'
                }
            }
        }
    }
}
