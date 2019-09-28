node{
 
   stage('SCM Checkout'){
     git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} sonar:sonar -Dsonar.host.url=http://35.163.30.67:9000/sonar/"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh "hostname"
     sh "whoami"
     sh "docker build -t gabrielgomezdelatorre/retodevopsgabo:B${BUILD_NUMBER} ."
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-hub-cred', variable: 'dockerHubPwd')]) {
        sh "docker login -u gabrielgomezdelatorre -p ${dockerHubPwd}"
     }
     sh "docker push gabrielgomezdelatorre/retodevopsgabo:B${BUILD_NUMBER}"
   }
    stage('Deploy'){
     def dockerStop = "sudo docker rm -f retodevops;"
     def dockerRun = "sudo docker run -p 8080:8080 -d --name retodevops gabrielgomezdelatorre/retodevopsgabo:B${BUILD_NUMBER}"
     sshagent(['server-desa']) {
       sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.20.31 ${dockerStop}"
       sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.20.31 ${dockerRun}"
     }
   }
   
   }
