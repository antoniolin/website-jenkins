pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/antoniolin/jenkins.git'
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
