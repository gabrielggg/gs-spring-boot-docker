node{
 
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Mvn Package'){
     withMaven(maven: 'maven-3') {

      // Run the maven build
      sh "mvn clean package"

    } 
   }
   
   }
