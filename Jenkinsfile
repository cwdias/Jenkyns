pipeline {

def remote = [:]
remote.name = "master01"
remote.host = "192.168.1.101"
remote.allowAnyHosts = true

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/cwdias/Jenkyns.git'
      }
    }
    
node {
    withCredentials([sshUserPrivateKey(credentialsId: 'master01-ssh-cred', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
        remote.user = userName
        remote.identityFile = identity
        stage("SSH Steps Rocks!") {
            writeFile file: 'abc.sh', text: 'ls'
            sshCommand remote: remote, command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
            sshPut remote: remote, from: 'abc.sh', into: '.'
            sshGet remote: remote, from: 'abc.sh', into: 'bac.sh', override: true
            sshScript remote: remote, script: 'abc.sh'
            sshRemove remote: remote, path: 'abc.sh'
        }
    }
}

    

  }

}
