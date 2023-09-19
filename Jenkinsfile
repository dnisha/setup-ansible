pipeline {
    agent any

    parameters {
        string(description: 'batianIp', name: 'batianIp', trim: true)
    }

    stages {

        stage('Setup ansible on bastian host') {

            steps {
                echo "SSH server IP is $batianIp"

                script {

                    sshagent(['ansible-server']) {

                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@${batianIp} '

                        sh 'scp * ubuntu@${batianIp}:/home/ubuntu'

                        sh """
                            ssh -o StrictHostKeyChecking=no ubuntu@${batianIp} '
                                sudo apt update -y &&
                                sudo apt install ansible -y &&
                                sudo apt-get install python3 -y &&
                                sudo apt-get install python3-pip -y &&

                                sudo pip3 install boto3 &&

                                sudo mkdir -p /etc/ansible &&
                                sudo mv ansible.cfg /etc/ansible/ansible.cfg &&
                                sudo mv aws_ec2.yaml /etc/ansible/aws_ec2.yaml'
                           """
                    }
                }
            }
        }

         stage('checkout ansible role') {

            steps {

                script {

                    sshagent(['ansible-server']) {

                        sh """
                            ssh -o StrictHostKeyChecking=no ubuntu@${batianIp} '
                                git clone https://github.com/dnisha/Hashicorp-vault-consul-integration.git'
                           """
                    }
                }
            }
        }
    }
}
