pipeline {
    agent any
    tools{
        maven "Maven 3.8.7"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git 'https://github.com/Manideepthaduri/Linux.git'
          
        } 
      }
      
  stage('Build the code') {
            steps {
                sh 'mvn clean install'
            }
        }    
      
 stage('Build Docker Image') {
            steps {
                sh '''
               docker build . --tag web-application:$BUILD_NUMBER
               docker tag web-application:$BUILD_NUMBER manideep9/wev-application:$BUILD_NUMBER
                
                '''
                
            }
        }
        stage('Push Docker Image') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'DockerHub_username_password', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                 sh '''
                 docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD
                 docker push mmreddy424/web-application:$BUILD_NUMBER
                    
                   ''' 
}
            }
            
        }
      
    }
}
