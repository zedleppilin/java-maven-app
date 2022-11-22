pipeline {
    agent any
    stages
    {
        stage("copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(['ansible-server-key']){
                        sh "scp -o StrictHostKeyChecking=no ansible/* ubuntu@3.93.11.42:/home/ubuntu "

                        withCredentials([sshUserPrivateKey(credentialsId: "ec2-server-key", keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                            sh 'scp  $keyfile ubuntu@3.93.11.42:/home/ubuntu/morrowindabyss-key-virginia-us-east-1.pem'
                            sh 'whoami'
                        } 
                    }
                }
            }
        }
        stage ("execute ansible playbook "){
            steps{
                script{
                    echo "calling ansible playbook to configure ec2 instances "
                    def remote = [:]
                    remote.name = "ubuntu"
                    remote.host = "3.93.11.42"
                    remote.allowAnyHosts = true


                    withCredentials([sshUserPrivateKey(credentialsId: "ansible-server-key", keyFileVariable: 'identity', usernameVariable: 'userName')]){
                        remote.user = userName
                        remote.identityFile = identity
                        sshCommand remote: remote, command:" ls -l" 
                    }
                }   
            }
        }
    }
}
