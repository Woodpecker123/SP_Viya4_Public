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
    stage('Docker Config') {
      steps {
        sh 'docker login sbi202212.azurecr.io --username=sbi202212 --password=xsNEG1u4q3Fx1OiWdQ0ZclerHarwOW5FpRPS1MXi00+ACRCLRbre'
        echo 'Docker succesfully Logged in'
        sh 'docker pull sbi202212.azurecr.io/viya-4-x64_oci_linux_2-docker/sas-orchestration:1.86.3-20221216.1671216783534'
        sh 'docker tag sbi202212.azurecr.io/viya-4-x64_oci_linux_2-docker/sas-orchestration:1.86.3-20221216.1671216783534 sas-orchestration'
        echo 'Docker image succesfully Pulled'
        //sh 'cd ./operator_deploy && kubectl -n sasoperator create secret generic sas-orchestration-secret --type=kubernetes.io/dockerconfigjson   --from-file=.dockerconfigjson=site-config/image-pull-secret.json'
      }
    }

  }
}
