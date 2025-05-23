pipeline {
    agent any

    stages {
        stage('Terraform Init & Apply') {
            steps {
                echo "Terraform Stage"
                sh 'terraform init'
                sh 'terraform apply -auto-approve'
            }
        }

        stage('Ansible Provisioning') {
            steps {
                echo "Ansible Stage"
                ansiblePlaybook(
                    colorized: true,
                    credentialsId: 'SSH_Ubuntu_id_rsa',
                    inventory: 'inventory.ini',   // replace with your actual inventory file
                    playbook: 'site.yml',         // replace with your actual playbook file
                    vaultTmpPath: ''
                )
            }
        }
    }
}
