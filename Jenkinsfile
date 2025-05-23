pipeline {
    agent any

    environment {
        TF_DIR = './'
        ANSIBLE_DIR = './'
    }

    stages {
        stage('Terraform Init & Apply') {
            steps {
                sh 'terraform init'
                sh 'terraform apply -auto-approve'
                }
            }
        }

        stage('Ansible Provisioning') {
            steps {
                ansiblePlaybook colorized: true, credentialsId: 'SSH_Ubuntu_id_rsa', inventory: './', playbook: './', vaultTmpPath: ''
                }
            }
        }
    }
}
