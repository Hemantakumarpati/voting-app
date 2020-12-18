pipeline {
  environment {
    registry = "hemantakumarpati/votingapp"
    registryCredential = 'dockeruser'
    dockerImage = ''
 }
  agent any
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t hemantakumarpati/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t hemantakumarpati/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t hemantakumarpati/worker ./worker'
      }
    }
    stage('Push result image') {
       steps {
          withCredentials([usernamePassword( credentialsId: 'dockeruser', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          docker.withRegistry('https://registry.hub.docker.com', 'dockeruser') {
          sh "docker login -u ${USERNAME} -p ${PASSWORD}"
          dockerImage.push("$BUILD_NUMBER")
          dockerImage.push hemantakumarpati/result
        }
      }
    }
    stage('Push vote image') {
       steps {
        withDockerRegistry(credentialsId: 'registry.hub.docker.com', url:'') {
          sh 'docker push hemantakumarpati/vote'
        }
      }
    }
    stage('Push worker image') {
       steps {
        withDockerRegistry(credentialsId: 'registry.hub.docker.com', url:'') {
          sh 'docker push hemantakumarpati/worker'
        }
      }
    }
  }
}
