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
        withDockerRegistry(credentialsId: 'https://registry.hub.docker.com', 'dockeruser') {
          sh 'docker push hemantakumarpati/result'
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
