pipeline {
    agent any
    stages {
        stage("copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(['ansible-server-key']){
                        sh "scp -o StrictHostKeyChecking=no ansible/* ubuntu@3.93.11.42:/home/ubuntu "

                        withCredentials([sshUserPrivateKey(credentialsId:"ec2-server -key", keyFileVariable: 'keyfile','username')]){
                            sh "scp -o ${keyfile} ubuntu@3.93.11.42:/home/ubuntu/morrowindabyss-key-virginia-us-east-1.pem"
                        }
                    }
                }
            }
        }
    }
}