stage('Install kubectl') {
  steps {
    sh '''
      set -e
      cd "$WORKSPACE"

      # Download kubectl to workspace
      KVER=$(curl -L -s https://dl.k8s.io/release/stable.txt)
      curl -L -o kubectl "https://dl.k8s.io/release/${KVER}/bin/linux/amd64/kubectl"
      chmod +x kubectl

      ./kubectl version --client=true
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
