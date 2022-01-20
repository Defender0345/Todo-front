#!groovy

pipeline {
  agent {
    docker {
      image 'node:lts-alpine'
    }
  }
  environment {
    HOME = '.'
    dockerImage = ''
  }
  stages {
    stage ('Clone Git') {
      steps {
        git 'https://github.com/Defender0345/Todo-front.git'
      }
    }
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