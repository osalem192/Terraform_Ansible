pipeline {
    agent {
        docker {
            image 'hashicorp/terraform:1.9.7'  // Official Terraform image
            args '--entrypoint=""'             // Override entrypoint for compatibility
        }
    }

    environment {
        AWS_REGION = 'us-east-1'              // Adjust if needed
    }

    stages {
        stage('Terraform Init & Apply') {
            steps {
                script {
                    echo "Using Terraform Stage"
                }
                withCredentials([usernamePassword(
                    credentialsId: 'AWS_credentials',
                    usernameVariable: 'AWS_ACCESS_KEY_ID',
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                )]) {
                    sh '''
                        terraform init
                        terraform apply --auto-approve
                    '''
                }
            }
        }

        stage('Ansible Provisioning') {
            agent any  // Use a different agent for Ansible if needed
            steps {
                echo "Ansible Stage"
                ansiblePlaybook(
                    colorized: true,
                    credentialsId: 'SSH_Ubuntu_id_rsa',
                    inventory: 'inventory',      // Replace with actual inventory file path
                    playbook: 'play_0.yml',      // Replace with actual playbook
                    vaultTmpPath: ''
                )
            }
        }
    }
}
