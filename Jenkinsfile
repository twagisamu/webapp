pipeline {
  agent any

  environment {
    IMAGE = "twagisamu/webapp-jenkins:v1"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'echo "npm test"'
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t $IMAGE .'
      }
    }

    stage('Docker Push') {
      steps {
        withCredentials([
          usernamePassword(
            credentialsId: 'dockerhub',
            usernameVariable: 'USER',
            passwordVariable: 'PASS'
          )
        ]) {
          sh 'echo $PASS | docker login -u $USER --password-stdin'
        }
        sh 'docker push $IMAGE'
      }
    }
  }
}