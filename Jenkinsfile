pipeline {
    agent any

    stages {
        stage('Build') {
            steps{
                echo 'Build'
            }
            }
          
           stage ('Test') {
            steps {
                echo 'Testing Phase'
                sh '''
                    ls -la
                    node --version
                    npm --version
                '''
                }
            }
        }
}