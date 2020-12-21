pipeline {
  //environment {
    //registry = "hemantakumarpati/votingapp"
    //registryCredential = 'dockeruser'
    //dockerImage = ''
// }
  agent any
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t hemantakumarpati/result ./result'
      }
    } 
   stage('Push result image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}
          sh "docker push hemantakumarpati/result:latest"
        }
      }
    }
 }
