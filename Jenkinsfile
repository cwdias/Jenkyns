pipeline {

  environment {
     registry = "master01:9443/nginx:latest"
     dockerImage = ""
     JOB_NAME = "${JOB_NAME}".replace("-deploy", "") 
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
  }
}
