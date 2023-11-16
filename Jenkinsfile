pipeline {
  environment {
    registry = "salaheddineadmou/devops"
    registryCredential = 'salaheddineadmou'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/salahEddine-Admou/salahEddine-Admou.git'
      }
    }
    stage('Build') {
       steps {
         sh 'docker build -t simple-web-application .'
       }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( 'https://hub.docker.com/r/salaheddineadmou/devops', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}