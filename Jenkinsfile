pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/gucgit/terraformtestforvpc.git'
            }
        }

        stage('Install Terraform') {
            steps {
                sh '''
                sudo apt update
                sudo apt install -y software-properties-common gnupg2 curl unzip
                curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
                sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
                sudo apt-get update && sudo apt-get install -y terraform
                terraform -version
                '''
            }
        }

        stage('Initialize Terraform') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Validate Terraform') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Apply Terraform') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
    }

    post {
        success {
            echo 'Terraform deployment successful!'
        }
        failure {
            echo 'Terraform deployment failed!'
        }
    }
}
