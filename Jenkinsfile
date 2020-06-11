pipeline {

  environment {
    registry = "localhost:5000/antonio/http-server-v1"
    dockerImage = ""
  }

  agent {
    dockerfile true
  }

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/antoniolin/website-jenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "nginx-server.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
