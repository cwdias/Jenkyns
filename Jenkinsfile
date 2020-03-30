pipeline {

  environment {
     registry = "master01:9443/nginx:latest"
     dockerImage = "" 
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/cwdias/Jenkyns.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry('https://master01:9443', 'docker-regist-cred') {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig-cred", enableConfigSubstitution: true)
        }
      }
    }

    stage('Dangling Images') {
      steps {
         sh 'docker image rm nginx:latest'
      }
    }
    
    stage('Get Pods') {
      steps {
         sh 'ssh -o StrictHostKeyChecking=no root@192.168.1.101 while [[ $(kubectl get pods -l app=nginx -o 'jsonpath={..status.conditions[?(@.type=="Ready")].status}') != "True" ]]; do echo "waiting for pod" && sleep 1; done'
         sh 'ssh -o StrictHostKeyChecking=no root@192.168.1.101 kubectl get pods -o wide'
      }
    }
  }
}
