pipeline {
    agent any

    stages {
        /*
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        */
        stage('E2E'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.51.1-noble'
                    reuseNode true
                }
            }
            steps{
                
                echo 'Test Stage'
                sh '''
                   npm install -g serve
                   serve -s build
                   npx playwright test
                '''
                
            }
        }
    

    }

    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
    
}
