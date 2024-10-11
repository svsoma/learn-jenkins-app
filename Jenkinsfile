pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'c2afd931-d73f-4dda-b9da-d0f6be333864'
    }
 
      stages {     
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm install
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        
        stage('Stage Tests') {
            parallel {
              stage('Unit Test') {
                agent {
                    docker {
                        image 'node:18-alpine'
                        reuseNode true
                    }
                }

                steps {
                    sh '''
                        test -f build/index.html
                        npm test
                    '''
                }
                post {
                    always {
                        junit 'just-results/junit.xml'
                    }
                }
            }
            /*
            stage('E2E') {
                agent {
                    docker {
                        image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                        reuseNode true
                    }
                }

                steps {
                    sh '''
                        npm install serve
                        node_modules/.bin/serve -s build &
                        sleep 10
                        npx playwright test --reporter=html
                    '''
                } */
            
            post {
                always {
                    publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'playwright-report', reportFiles: 'index.html', reportName: 'Playwright HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                    }
            }
        }
        }
    
        stage('Deploy') {
            agent {
                docker {
                        image 'node:18-alpine'
                        reuseNode true
                        }
            }
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploying to production.  Site ID: $NETLIFY_SITE_ID"
                 '''
               }
            }
    }
}