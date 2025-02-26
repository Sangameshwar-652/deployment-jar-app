pipeline {
    agent any

    environment {
        SERVER_IP = credentials('prod-server-ip')
    }
    stages {
        stage('Setup') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('Test') {
            steps {
                  sh "mvn test"
            }
        }

        stage('Deploy to Prod') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key', keyFileVariable: 'MY_SSH_KEY', usernameVariable: 'username')]) {
                    sh '''
                    scp -i $MY_SSH_KEY -o StrictHostKeyChecking=no target/myapp.war  ${username}@${SERVER_IP}:}:/opt/tomcat/webapps/
                    ssh -i $MY_SSH_KEY -o StrictHostKeyChecking=no ${username}@${SERVER_IP} << EOF
                        sudo systemctl restart tomcat

EOF
                    '''
                }
            }
        }
       
        
       
        
    }
}
