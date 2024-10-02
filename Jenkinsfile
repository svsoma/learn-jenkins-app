pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
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