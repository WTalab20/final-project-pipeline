pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Deploy K8s YAMLs') {
      steps {
        sh 'kubectl apply -f mysql-pv.yaml'
      }
    }
  }
}
