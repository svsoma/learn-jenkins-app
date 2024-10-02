pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    reuseNode true
                }
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