pipeline {
    agent any
    
    environment {
        SSH_KEY = credentials('hpuser-ssh-key')
        VAULT_PASS = credentials('ansible-vault-password')
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                sh """
                echo "\$VAULT_PASS" > .vault_pass.txt
                ansible-playbook -i inventory playbook.yml --private-key=\$SSH_KEY --vault-password-file .vault_pass.txt
                rm -f .vault_pass.txt
                """
            }
        }
    }
    
    post {
        success {
            echo "Patching process completed successfully!"
        }
        failure {
            sh "rm -f .vault_pass.txt"
            echo "Patching process failed. Please check the console logs."
        }
    }
}
