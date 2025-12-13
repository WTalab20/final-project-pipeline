node {
  stage('Checkout') {
    checkout scm
  }

  stage('Install kubectl') {
    sh '''
      set -e
      cd "$WORKSPACE"

      echo "Downloading kubectl..."
      KVER=$(curl -sL https://dl.k8s.io/release/stable.txt)
      curl -sL -o kubectl "https://dl.k8s.io/release/${KVER}/bin/linux/amd64/kubectl"
      chmod +x kubectl
      ./kubectl version --client=true
    '''
  }

  stage('Deploy K8s YAMLs') {
    sh '''
      set -e
      cd "$WORKSPACE"

      echo "=== Files in workspace ==="
      ls -la

      echo "=== Find YAML files ==="
      find . -maxdepth 5 -type f \\( -name "*.yml" -o -name "*.yaml" \\) -print

      echo "=== Apply mysql PV if found ==="
      if [ -f mysql-pv.yaml ]; then
        ./kubectl apply -f mysql-pv.yaml
      elif [ -f k8s/mysql-pv.yaml ]; then
        ./kubectl apply -f k8s/mysql-pv.yaml
      elif [ -f manifests/mysql-pv.yaml ]; then
        ./kubectl apply -f manifests/mysql-pv.yaml
      else
        echo "ERROR: mysql-pv.yaml not found anywhere in repo."
        exit 1
      fi
    '''
  }
}
