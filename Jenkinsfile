node{
 
   stage('SCM Checkout'){
     git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Análisis Sonar'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} sonar:sonar -Dsonar.host.url=http://172.31.21.126:9000/sonar/"
   }
   stage('MVN Unit testing & Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh "docker build -t gabrielgomezdelatorre/retodevopsgabo:Build${BUILD_NUMBER} ."
   }
   stage('Push Docker Image a DockerHub'){
     withCredentials([string(credentialsId: 'docker-hub-cred', variable: 'dockerHubPwd')]) {
       sh "docker login -u gabrielgomezdelatorre -p ${dockerHubPwd}"
     }
     sh "docker push gabrielgomezdelatorre/retodevopsgabo:Build${BUILD_NUMBER}"
   }
   stage('Deploy'){
     try {
       def dockerDestroy = "sudo docker rm -f retodevops;"
       sshagent(['server-desa']) {
         sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.26.235 ${dockerDestroy}"
    }
   } catch (error) {
      echo "no hay contenedor";
   } finally {
       def dockerRun = "sudo docker run -p 8080:8080 -d --name retodevops gabrielgomezdelatorre/retodevopsgabo:Build${BUILD_NUMBER}"
       sshagent(['server-desa']) {
         sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.26.235 ${dockerRun}"
     }
   }
   }
    stage('Jmeter'){
     build job: 'Jmeter'
     }
 
}
