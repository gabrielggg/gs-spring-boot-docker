node{
       
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Mvn Package'){
       echo 'Hello, Maven'
       sh 'mvn --version'
   }
   
}
