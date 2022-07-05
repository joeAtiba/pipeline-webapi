pipeline {
    agent any
    
    environment {
        registryName = 'acraucppoctest'
        dockerFilePath = './webapi/'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/joeAtiba/webapi']]])
            }
        }
        
        stage ('Build Docker Image') {
            steps {
                script {
                    // You can't use strings here, use environment up above!
                    dockerImage = docker.build(registryName, dockerFilePath)
               }
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning up docker residue...'
            sh 'docker system prune -f            
        }
    }
}
