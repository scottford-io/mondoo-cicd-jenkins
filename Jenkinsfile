pipeline {
  environment {
    registry = "thesecureautomator/python-flask-app-demo"
    registryCredential = 'docker_hub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Build Docker Image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push Docker Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused Docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}