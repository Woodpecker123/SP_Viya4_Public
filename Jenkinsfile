pipeline {
  agent any
    environment {
    KUBECONFIG = '/var/lib/jenkins/kubeconfigaz'
  }
  stages {
    stage('') {
      steps {
        echo 'Hellooo'
      }
    }
        stage('Deployment Operator') {
      steps {
        //sh 'kubectl create ns sasoperator'
        sh 'cd ./operator_deploy && kustomize build . | kubectl -n sasoperator apply -f -'
        echo 'Deployment Operator succesfully deployed'
      }
    }

  }
}
