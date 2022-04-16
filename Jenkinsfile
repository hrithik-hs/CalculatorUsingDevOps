pipeline {
    agent any

    stages {
        stage('Github Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/hrithik-hs/CalculatorUsingDevOps'
            }
        }
        stage('Maven build') {
            steps {
                script{
                    sh 'mvn clean install'
                }
            }
        }
        stage('Docker build') {
            steps{
                script {
                    imageName=docker.build "hrithikhs/scientific_calculator_with_devops"
                }
            }
        }
        stage('Docker push img') {
            steps {
                script{
                    docker.withRegistry('','Docker_credentials'){
                    imageName.push()
                    }
                }    
            }
        }
        stage('ansible pull img') {
            steps {
                ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'inventory', playbook: 'p2.yml', sudoUser: null
            }    
        }
    }
}
