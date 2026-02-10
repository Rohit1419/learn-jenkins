pipeline {
    agent any

    stages {
        stage("without Docker"){
            steps{
                sh""" 
                echo without docker 
                touch container-no.txt
                """
            }
        }
        
        stage('with docker Node Build') {
            agent{
                docker{
                    image 'node:24-alpine'
                    reuseNode true
                }
            }
            steps {
                sh """
                echo with docker 
                node -v
                npm -v
                touch container-yes.txt
                
                """
                
            }
        }
    }
}
