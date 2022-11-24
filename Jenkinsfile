pipeline {
    agent any
    stages
    {
        stage("copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(credentials:['pubkey-to-ansible-server']){
                        sh "scp -o StrictHostKeyChecking=no ansible/* ansible@172.16.26.201:/home/ansible"

                        withCredentials(sshUserPrivateKey(credentialsId:'under-ansible',keyFileVariable: 'keyfile',username: 'user ')){
                            sh "scp ${keyfile} ansible@172.16.26.201:/home/ansible/ssh-key.pem "
        
                        }
                    }     
                }

            }   
            
        }
    }
}
