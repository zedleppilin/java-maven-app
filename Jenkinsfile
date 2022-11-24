pipeline {
    agent any
    stages
    {
        stage("copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(['ggwp']){
                        sh " sshpass -p 'ansible' scp -o StrictHostKeyChecking=no ansible/* ansible@172.16.26.201:/home/ansible"

                        withCredentials([sshUserPrivateKey(credentialsId:'under-ansible',keyFileVariable: 'keyfile',username: 'user')]){
                            sh 'sshpass -p "ansible" scp $keyfile ansible@172.16.26.201:/home/ansible/ssh-key.pem '
        
                        }
                    }     
                }

            }   
            
        }
        stage("execute ansible pb"){
            steps {
                script{
                    echo "calling to configure servers" 
                    def remote=[:]
                    remote.name = "under-server"
                    remote.hosts = "172.16.26.201"
                    remote.allowAnyHosts = true
                    remote.user

                    sshCommand remote: remote, command : "ls -l"

                }
            }



    
        }
    }
}
