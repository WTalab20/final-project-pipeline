pipeline {
  agent any
  stages {
    stage('Checkout') { steps { checkout scm } }

    stage('Deploy K8s YAMLs') {
      steps {
        sh '''
          ls -la
          kubectl apply -f mysql-pv.yaml
          kubectl apply -f mysql-pvc.yaml
          kubectl apply -f mysql-configmap.yaml
          kubectl apply -f mysql-deployment.yaml

          kubectl apply -f nexus-deployment.yaml
          kubectl apply -f nexus-service.yaml

          kubectl apply -f jenkins-deployment.yaml
          kubectl apply -f jenkins-service.yaml

          kubectl apply -f webapp-configmap.yaml
          kubectl apply -f webapp-deployment.yaml
          kubectl apply -f webapp-service.yaml

          kubectl get pods -o wide
          kubectl get svc
        '''
      }
    }
  }
}
