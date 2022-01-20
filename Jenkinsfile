#!groovy

pipeline {
  environment {
    dockerImage = ''
  }
  agent any
  stages {
    stage ("Docker Build"){
      agent any
      steps {
        sh 'docker build -t todofront:1.0'
      }
    }
    stage ("runimage") {
      agent any
      steps {
        sh 'docker run --network nginxproxymanager_default --name=todofront todofront'
      }
    }
  }
}