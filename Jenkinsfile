pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('shehuawwal-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
//         sh 'docker build -t shehuawwal/lutz-nodejs:latest .'
        sh 'docker build -t shehuawwal/lutz-nodejs:$BUILD_NUMBER .'

      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push shehuawwal/lutz-nodejs:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
