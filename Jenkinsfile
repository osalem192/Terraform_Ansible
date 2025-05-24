pipeline {
    agent none  // Do NOT use a global Docker agent

    stages {
        stage('Terraform Init & Apply') {
            agent {
                docker {
                    image 'hashicorp/terraform:1.9.7'
                    args '--entrypoint=""'
                }
            }
            steps {
                script {
                    echo "Using Terraform Stage"
                }

                withCredentials([
                    usernamePassword(
                        credentialsId: 'AWS_credentials',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    ),
                    string(credentialsId: 'SSH_id_rsa_private', variable: 'TF_VAR_SSH_Key_private'),
                    string(credentialsId: 'SSH_id_rsa_public', variable: 'TF_VAR_SSH_Key_public')
                ]) {
                    sh '''
                        export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                        export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                        terraform init
                        terraform apply --auto-approve -input=false \
                          -var="SSH_Key_private=$TF_VAR_SSH_Key_private" \
                          -var="SSH_Key_public=$TF_VAR_SSH_Key_public"
                    '''
                }
            }
        }

    stage('Ansible Provisioning') {
        agent any
        steps {
            echo "Ansible Stage"
            echo "Finished Successfully"
        }
    }
    }
}
