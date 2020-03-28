pipeline {

node {
  sshagent (credentials: ['master01-ssh-cred']) {
    sh 'ssh -o StrictHostKeyChecking=no root@192.168.1.101 uname -a'
  }
}

}
