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
        withDockerRegistry([credentialsId: 'dockeruser', url: 'https://registry.hub.docker.com']) {
          sh "docker login -u hemantakumarpati -p Master@1927"
          sh 'docker push hemantakumarpati/result'
        }
      }
    }
    
    stage('Push vote image') {
       steps {
        withDockerRegistry([credentialsId: 'dockeruser', url: 'https://registry.hub.docker.com']) {
          sh "docker login -u hemantakumarpati -p Master@1927"
          sh 'docker push hemantakumarpati/vote'
        }
      }
    }
    stage('Push worker image') {
       steps {
        withDockerRegistry([credentialsId: 'dockeruser', url: 'https://registry.hub.docker.com']) {
          sh "docker login -u hemantakumarpati -p Master@1927"
          sh 'docker push hemantakumarpati/worker'
        }
      }
    }
  }
}
