pipeline {
    agent any

    stages {
        
        stage('Build-Docker') {
            agent{
                docker{
                    image 'node:24-alpine'
                    reuseNode true
                }
            }
            steps {
                    sh """
                    ls -la 
                    node -v
                    npm -v
                    npm ci
                    npm run build
                    ls -la
                
                """
                
            }
        }

        stage("Test"){
            agent{
                docker{
                    image 'node:24-alpine'
                    reuseNode true
                }
            }
            steps{
                sh"""
                    test -f build/index.html
                    echo "File exists, running tests..."
                    npm test

                """
            }
        }

                stage("E2E Test"){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-noble'
                    reuseNode true
                }
            }
            steps{
                sh"""
                    npm install serve 
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test 

                """
            }
        }
    }

    post{
        always{
            junit 'jest-results/junit.xml'
        }
    }
}
