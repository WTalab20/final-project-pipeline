stage('Deploy K8s YAMLs') {
  steps {
    sh '''
      set -e
      cd "$WORKSPACE"

      echo "=== Files in workspace ==="
      ls -la

      echo "=== Find YAML files ==="
      find . -maxdepth 3 -type f \\( -name "*.yml" -o -name "*.yaml" \\) -print

      echo "=== Try applying common locations ==="
      if [ -f mysql-pv.yaml ]; then
        ./kubectl apply -f mysql-pv.yaml
      elif [ -f k8s/mysql-pv.yaml ]; then
        ./kubectl apply -f k8s/mysql-pv.yaml
      elif [ -f manifests/mysql-pv.yaml ]; then
        ./kubectl apply -f manifests/mysql-pv.yaml
      else
        echo "ERROR: mysql-pv.yaml not found. Check the file list above."
        exit 1
      fi
    '''
  }
}
