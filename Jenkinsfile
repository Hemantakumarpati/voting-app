pipeline {
   agent any

  stages {
    stage('Build result') {
      steps {
        sh "docker build -t hemantakumarpati/result:${env.BUILD_NUMBER} ./result"
      }
    } 
    stage('Build vote') {
      steps {
        sh "docker build -t hemantakumarpati/vote:${env.BUILD_NUMBER} ./vote"
      }
    }
    stage('Build worker') {
      steps {
       sh "docker build -t hemantakumarpati/worker:${env.BUILD_NUMBER} ./worker"
      }
    }
   stage('Push result image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push hemantakumarpati/result:${env.BUILD_NUMBER}"
        }
      }
    }
    stage('Push vote image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push hemantakumarpati/vote:${env.BUILD_NUMBER}"
        }
      }
    }
    stage('Push worker image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push hemantakumarpati/worker:${env.BUILD_NUMBER}"
        }
      }
    }
    stage('Deploy on test') {
         steps {
            script {
               env.PIPELINE_NAMESPACE = "default"
               //kubernetesDeploy(kubeconfigId: 'mykubeconfig', configs: 'k8s-specifications/')
                withKubeConfig([credentialsId: 'mykubeconfig', serverUrl: 'https://10.128.0.31:6443']) {
                sh 'kubectl apply -f k8s-specifications'
            }
         }
      }
                                }
}
}
