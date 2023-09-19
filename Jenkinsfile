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
                sh 'scp * ubuntu@${batianIp}:/home/ubuntu'
                sh 'chmod +x setup-ansible.sh'
                }
                echo 'Hello World'
            }
        }

        stage('Run Script') {
            steps {
                sshagent(['ansible-server']) {

                sh 'ssh -o StrictHostKeyChecking=nossh ubuntu@${batianIp}:/home/ubuntu/setup-ansible.sh'

                }
            }
        }
    }
}
