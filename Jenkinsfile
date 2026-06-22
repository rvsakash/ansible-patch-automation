pipeline {
    agent any
    
    environment {
        // Jenkins credential ID ko variable me set kiya
        SSH_KEY = credentials('hpuser-ssh-key')
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Yeh aapke GitHub repository se latest code pull karega
                checkout scm
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                // Yeh command target servers par patching run karega
                sh "ansible-playbook -i inventory playbook.yml --private-key=\$SSH_KEY"
            }
        }
    }
    
    post {
        success {
            echo "Patching process successfully complete ho gaya hai!"
        }
        failure {
            echo "Patching process fail ho gaya hai. Kripya console logs check karein."
        }
    }
}

