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
                    export PATH=$PATH:/usr/local/bin
                    node --version
                    npm --version
                '''
                }
            }
        }
}