pipeline {
   agent any

  stages {
    stage('Build result') {
      steps {
        sh "docker build -t hemantakumarpati/result:${env.BUILD_NUMBER} ."
      }
    } 
    stage('Build vote') {
      steps {
        sh "docker build -t hemantakumarpati/vote:${env.BUILD_NUMBER} ."
      }
    }
    stage('Build worker') {
      steps {
       sh "docker build -t hemantakumarpati/worker:${env.BUILD_NUMBER} ."
      }
    }
   stage('Push result image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push hemantakumarpati/result:latest"
        }
      }
    }
    stage('Push vote image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push hemantakumarpati/vote:latest"
        }
      }
    }
    stage('Push worker image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push hemantakumarpati/worker:latest"
        }
      }
    }
 }
