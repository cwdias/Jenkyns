pipeline {

  environment {
    registry = "master01:9443/nginx:v1"
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
  	    sshagent (credentials: ['master01-ssh-cred']) {
    		  sh 'ssh -o StrictHostKeyChecking=no -l cloudbees 192.168.1.101 hostname'
  	    }
      }
    }

    

  }

}
