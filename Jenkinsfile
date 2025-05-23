pipeline {
    agent {
        docker {
            image 'hashicorp/terraform:1.9.7' // Official Terraform image
            args '--entrypoint=""' // Override entrypoint for Jenkins compatibility
        }
    }

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
