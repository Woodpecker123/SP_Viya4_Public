pipeline {
  agent any
    environment {
    KUBECONFIG = '/var/lib/jenkins/kubeconfigaz'
  }
  stages {
    stage('Test') {
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
//      stage('Docker Run') {
//       steps {
//         sh 'docker run --rm -v $(pwd):/var/lib/jenkins/workspace/SP_Viya4_Public/ sas-orchestration create sas-deployment-cr  --deployment-data /var/lib/jenkins/workspace/SP_Viya4_Public/license/SASViyaV4_9CNG4B_certs.zip  --license /var/lib/jenkins/workspace/SP_Viya4_Public/llicense/SASViyaV4_9CNG4B_1_stable_2022.12_license_2022-12-25T061859.jwt  --user-content /var/lib/jenkins/workspace/SP_Viya4_Public/viya4/ --cadence-name stable --cadence-version 2022.12 --image-registry  sbi202212.azurecr.io --repository-warehousehttp://10.0.128.8:80/ocp4/ > viya4-sasdeployment.yaml'
//         echo 'Docker run for Viya 4 Deployment succesfully created'
//       }
//     }
      stage('Deploy') {
      steps {
        sh 'kubectl -n sasoperator apply -f viya4-sasdeployment.yaml'
        echo 'Viya 4 Deployment succesfully Completed'
//         sh 'kubectl -n sasoperator get pods'
//         echo 'Please Check status of Pods on the Cluster'
      }
    }

  }
}
