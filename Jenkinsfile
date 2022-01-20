node {
  def app

  stage('Clone repo') {
    checkout scm
  }

  stage('Build Image') {
    app = docker.build("defender/todofront")
  }

  stage('Test') {
    app.inside {
      sh 'echo "Tests Passed"'
    }
  }
}
// pipeline {
//   agent any
//   stages {
//     stage ('add docker') {
//       agent {
//         docker {
//           image node:lts-alpine
//         }
//       }
//     }
//     stage ("buildimage"){
//       steps {
//         sh 'docker build -t todofront:1.0'
//       }
//     }
//     stage ("runimage") {
//       steps {
//         sh 'docker run --network nginxproxymanager_default --name=todofront todofront'
//       }
//     }
//   }
// }