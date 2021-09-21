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
                
                git 'https://github.com/siji-sathyan/angapp1.git'
                
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
      stage('docker-build') {
            steps {
              script{
                docker.withTool('docker'){
                  sh 'docker version'
                  sh 'docker buid -t sijisdocker/angapp1:v1 .'
                  
                }
            }
        }
    }
}
}


