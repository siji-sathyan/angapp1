pipeline {
    agent {label 'agent' }
    
    tools {
    nodejs 'NodeJS'
      dockerTool 'docker'
     
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
                  sh 'docker build -t angapp1 .'
                  sh 'docker tag angapp1 sijisdocker/angapp1:angapp1'
                }
            }
        }
    }
      stage('docker-login'){
        steps{
          
            withCredentials([string(credentialsId: 'DOCKER_HUB', variable: 'PASSWORD')]) {
              sh "docker login -u sijisdocker -p ${PASSWORD}"
     
        
      }
      }
      }
}
}


