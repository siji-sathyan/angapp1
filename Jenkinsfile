pipeline {
    agent {label 'agent' }
    
    tools {
    nodejs 'NodeJS'
    } 
    environment {
        CI = 'true'
    }

    stages {
        stage('checkout') {
            steps {
                
                git 'https://github.com/siji-sathyan/ang-project.git'
                
            }
        }
         stage('npm install') {
            steps {
                
               sh 'npm install'
                
            }
        }
         stage('build') {
            steps {
                
              sh 'npm run build'
            
                
            }
        }
    }
}


