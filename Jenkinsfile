pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                   # image 'node:18-alpine'
                   # reuseNode true
                }
            }
          
           stage ('Test') {
            steps {
                echo 'Testing Phase'
                sh '''
                    ls -la
                    npm --version
                    npm test
                '''
                }
            }
        }
    }
}