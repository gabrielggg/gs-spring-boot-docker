node{
 
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/javahometech/my-app'
   }
   stage('Mvn Package'){
     withMaven(maven: 'maven-3') {

      // Run the maven build
      sh "mvn clean package"

    } 
   }
   
   }
