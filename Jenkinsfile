pipeline {
    agent any
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
    }
}
