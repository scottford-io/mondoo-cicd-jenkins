pipeline {
  environment {
    registry = "thesecureautomator/mondoo-scanned-python-flask-app"
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
    stage('Scan Docker Image with Mondoo') {
      environment {
        MONDOO_CLIENT_ACCOUNT = credentials('MONDOO_CLIENT_ACCOUNT')
      }
      steps{
        sh "env | sort"
        sh "echo ${MONDOO_CLIENT_ACCOUNT} | base64 -d > mondoo.json"
        sh 'curl -sSL https://mondoo.io/download.sh | sh'
        sh "./mondoo scan dockeer $registry:$BUILD_NUMBER --config mondoo.json"
      }
    }
    stage('Remove Unused Docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}