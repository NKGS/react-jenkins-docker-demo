// node {
//     def app
//     stage('Clone Repository') {
//         checkout scm
//     }

//     stage('Build Image') {
//         app = docker.build("lovetwocode/react-docker-jenkins")
//     }

//     stage('Test Image') {
//         app.inside {
//             echo "Test passed"
//         }
//     }

//     stage('Push Image') {
//         withDockerRegistry([ credentialsId: "docker-hub", url: "" ]) {
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//         }
//         echo "Trying to push docker build to dockerhub"
//     }
// }

pipeline {
  agent { label 'docker' } 
  stages {
    stage('Build') {
      steps {
        sh docker build . -t "lovetwocode/react-docker-jenkins"
      }
    }
    stage('Publish') {
      when {
        branch 'main'
      }
      steps {
        withDockerRegistry([ credentialsId: "docker-hub", url: "" ]) {
          sh 'docker push lovetwocode/react-docker-jenkins'
        }
      }
    }
  }
}


//never used
// pipeline {
//     agent {
//         docker {
//             image 'node:6-alpine' 
//             args '-p 3000:3000' 
//         }
//     }
//     stages {
//         stage('Build') { 
//             steps {
//                 sh 'npm install' 
//             }
//         }
//     }
// }