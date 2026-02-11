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
    }

    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
