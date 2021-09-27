def dockerRun='docker run -p 80:80 -d --name angularapp1 sijisdocker/angapp1:v1'
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
      stage('build package') {
            steps {
                
              sh 'zip angapp1.zip dist/angapp1'
          
            }
         }
      stage('Artifact') {
            steps {
                fingerprint 'angapp1.zip'
                archiveArtifacts 'angapp1.zip'
          
            }
         }
      stage('docker-build') {
            steps {
              script{
                docker.withTool('docker'){
                  sh 'docker version'
                  sh 'docker build -t angapp1:v1 .'
                  sh 'docker tag angapp1:v1 sijisdocker/angapp1:v1'
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
      stage('push image to docker hub'){
        steps{
        sh 'docker push sijisdocker/angapp1:v1'
      }
      }
       stage('Run on server'){
        steps{
          
          sshagent(['SSH-ID']) {
            sh "ssh -o StrictHostKeyChecking=no ec2-user@18.234.248.132 ${dockerRun}"
      }

      }
      }
      
}
}


