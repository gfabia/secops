pipeline {
  agent any 

  stages {
    stage('Daily Compliance Run') {
      steps{
        echo 'Running a compliance scan with inspec....'
          script{
            def remote = [:]
            remote.name = "test-vm"
            remote.host = "10.128.0.2"
            remote.allowAnyHosts = true

            withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                remote.user = userName
                remote.identityFile = identity
                stage("Scan with InSpec") {
                  sshCommand remote: remote, sudo: true,  command: 'inspec exec  /root/linux-baseline/'
              }
            }
          }
       }
    }
  }
}