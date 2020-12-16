pipeline {
  environment {
    registry = "hemantakumarpati"
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
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(dockeruser: 'dockerbuildbot-index.docker.io', url:'') {
          sh 'docker push hemantakumarpati/result'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(dockeruser: 'dockerbuildbot-index.docker.io', url:'') {
          sh 'docker push hemantakumarpati/vote'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(dockeruser: 'dockerbuildbot-index.docker.io', url:'') {
          sh 'docker push hemantakumarpati/worker'
        }
      }
    }
  }
}
