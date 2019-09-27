node{
       tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: "maven-3", type: "maven"
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean install"
   }
   
}
