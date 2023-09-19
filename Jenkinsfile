pipeline {
    agent any

    parameters {
        string(description: 'batianIp', name: 'batianIp', trim: true)
    }

    stages {
        
        stage('Connecting with bastian host') {
            steps {
                sshagent(['ansible-server']) {
                
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@${batianIp}'
                sh 'scp setup-ansible/* ubuntu@${batianIp}:/home/ubuntu'
                }
                echo 'Hello World'
            }
        }
    }
}
