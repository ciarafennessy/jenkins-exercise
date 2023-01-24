pipeline {
  environment {
    NAMESPACE = "staging"
  }
  agent any
  stages {
   /* 
    stage('Install CLIs') {
      steps {
        sh "sudo chmod +x *.sh"
        sh "./install-cli.sh"
        sh "./install-eksctl.sh"
        sh "./install-kubectl.sh"
      }
    }
    */
    stage('Configure kubectl') {
      steps {
        sh "aws eks --region eu-west-2 update-kubeconfig --name Cluster1"
        sh "kubectl config set-context --current --namespace=${NAMESPACE}"
      }
    }
    stage('Deploy manifests') {
      steps {
        sh "kubectl apply -f backend.yaml"
        sh "kubectl apply -f frontend.yaml"
        sh "kubectl get services"
      }
    }
  }
}
