pipeline {

  agent {
    docker {
        image 'localhost:5000/antonio/http-server-v1'
        registryUrl 'localhost:5000'
    }
  }

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/antoniolin/website-jenkins.git'
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
