node('docker') {
    stage 'Checkout'
        checkout scm
    stage 'Build & UnitTest'
        sh "docker build -t todofront -f Dockerfile ."
}

// pipeline {
//   agent {
//     docker {
//       image 'node:lts-alpine'
//     }
//   }
//   environment {
//     HOME = '.'
//     dockerImage = ''
//   }
//   stages {
//     stage ('Clone Git') {
//       steps {
//         git 'https://github.com/Defender0345/Todo-front.git'
//       }
//     }
//     stage ("Docker Build"){
//       agent any
//       steps {
//         sh 'docker build -t todofront:1.0'
//       }
//     }
//     stage ("runimage") {
//       agent any
//       steps {
//         sh 'docker run --network nginxproxymanager_default --name=todofront todofront'
//       }
//     }
//   }
// }