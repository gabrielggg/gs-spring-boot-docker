node{
 
   stage('SCM Checkout'){
     git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} sonar:sonar -Dsonar.host.url=http://34.217.214.220:9000/sonar/"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh "hostname"
     sh "docker build -t gabrielgomezdelatorre/retodevopsgabo:B${BUILD_NUMBER} ."
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-hub-cred', variable: 'dockerHubPwd')]) {
        sh "docker login -u gabrielgomezdelatorre -p ${dockerHubPwd}"
     }
     sh "docker push gabrielgomezdelatorre/retodevopsgabo:B${BUILD_NUMBER}"
   }
   
   }
