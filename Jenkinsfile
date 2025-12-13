pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Show files') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh '''
          chmod +x deploy.sh
          ./deploy.sh
        '''
      }
    }
  }
}
