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
    stage ('Deploy') {
      steps{
        sshagent(credentials : ['ssh-agent-cred']) {
             sh 'ssh -o StrictHostKeyChecking=no -l root 192.168.1.101 uname -a'
        }
      }
    }
  }
}
