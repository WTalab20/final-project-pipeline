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

          # Download kubectl into workspace
          KVER=$(curl -sL https://dl.k8s.io/release/stable.txt)
          curl -sL -o kubectl "https://dl.k8s.io/release/${KVER}/bin/linux/amd64/kubectl"
          chmod +x kubectl

          ./kubectl version --client=true
        '''
      }
    }

    stage('Configure kubectl (in-cluster)') {
      steps {
        sh '''
          set -e
          echo "Using in-cluster Kubernetes config"
        '''
      }
    }

    stage('Deploy K8s YAMLs') {
      steps {
        sh '''
          set -e
          cd "$WORKSPACE"
          ./kubectl apply -f mysql-pv.yaml
        '''
      }
    }

  }
}
