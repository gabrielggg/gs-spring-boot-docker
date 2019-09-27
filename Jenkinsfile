node{
 
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/javahometech/my-app'
   }
   stage('Mvn Package'){
     withMaven() {

      // Run the maven build
      sh "mvn clean package"

    } 
   }
   
   }
