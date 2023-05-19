pipeline {

  environment {
    dockerimagename = "med00723/images"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'git branch: 'main', credentialsId: 'github-credentials', url: 'https://github.com/med00723/jenkins-kubernetes-deployment.git''
      }
    }

    stage('Build imagee') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

  

  }

}
