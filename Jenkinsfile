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
        sshagent(credentials : ['ssh-private-key']) {
            sh 'ssh -o StrictHostKeyChecking=no root@192.168.1.101 uptime'
            sh 'ssh -v root@192.168.1.101'
            sh 'hostname -I'
        }
      }
    }
  }
}
