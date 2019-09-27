node{
 
   stage('SCM Checkout'){
     git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh "sudo docker build -t retodevopsgabo:B${BUILD_NUMBER} ."
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-hub-cred', variable: 'dockerHubPwd')]) {
        sh "sudo docker login -u gabrielgomezdelatorre -p ${dockerHubPwd}"
     }
     sh "sudo docker push gabrielgomezdelatorre/retodevopsgabo:B${BUILD_NUMBER}"
   }
   
   }
