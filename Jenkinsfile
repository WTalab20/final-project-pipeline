pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

stage('Install kubectl') {
  steps {
    sh '''
      set -e
      cd "$WORKSPACE"
      curl -sLO "https://dl.k8s.io/release/$(curl -sL https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
      chmod +x kubectl
      ./kubectl version --client=true
    '''
  }
}

    stage('Deploy K8s YAMLs') {
      steps {
        sh 'kubectl apply -f mysql-pv.yaml'
      }
    }
  }
}
