
pipeline {
  agent any
  stages {
    stage ('add docker') {
      agent {
        docker {
          image node:lts-alpine
        }
      }
    }
    stage ("buildimage"){
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