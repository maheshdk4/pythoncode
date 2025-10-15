pipeline{
   agent any
  environment {
    IMAGE_NAME = 'maheshdk4/pythoncode'
  }
  stages{
    stage('checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/maheshdk4/pythoncode'
      }
    }
    stage('build docker image'){
      steps{
        sh "docker build -t %IMAGE_NAME%:latest ."
      }
    }
    stage('push to dockerhub'){
      steps{
        withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
      sh '''
      echo %DOCKER_PASS% |
      docker login -u %DOCKER_USER% --password-stdin
      docker push %IMAGE_NAME%:latest
      docker logout
      '''
      }                                  
      }
    }
    }
    
}
