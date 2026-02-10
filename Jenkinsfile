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
    }
}
