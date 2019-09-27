pipeline{
       agent none
       Stages{
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/gabrielggg/gs-spring-boot-docker.git'
   }
   stage('Mvn Package'){
       agent { docker 'maven:3-alpine' } 
       echo 'Hello, Maven'
       sh 'mvn --version'
   }
   
       }}
