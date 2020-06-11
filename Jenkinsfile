pipeline {

  agent { 
    label 'jnlp-slave'
    docker {
        image 'localhost:5000/antonio/http-server-v1'
        label 'check-test-v1'
        registryUrl 'localhost:5000'
    }
  }

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
