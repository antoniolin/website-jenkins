pipeline {

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
        docker.withRegistry('localhost:5000/antonio') {

        docker.image('http-server-v1').inside {
            sh 'make test'
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
