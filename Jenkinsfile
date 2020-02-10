pipeline {
  
  environment {
    registry = "192.168.2.10:5000/myweb"
    dockerImage = ""
  }
  
  agent any
  
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/mak241265/demo.git'
      }
  }
  
  stage('Build image') {
   steps{
    script {
      dockerImage = docker.build registry + ":$BUILD_NUMBER"
    }
   }
  }
  
  stage('Push Image') {
    steps{
      script {
         docker.withRegistry( "" ) {
           dockerImage.push()
         }
      }
    }    
  }
  
  stage('Deploy App') {
    steps {
      script {
        kubernetesDeploy(configs: "deploy.yaml", kubeconfigId: "mykubeconfig")
      }
    }
  }
 }
}
         
         
  
  
  
  
