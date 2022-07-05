pipeline {
    agent any
    
    environment {
        registryName = 'acraucppoctest'
        registryUrl = 'acraucppoctest.azurecr.io'
        registryCredential = 'AcrAucpTest'
        dockerFilePath = './webapi/'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/joeAtiba/webapi']]])
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // You can't use strings here, use environment up above!
                    dockerImage = docker.build(registryName, dockerFilePath)
               }
            }
        }
        
        stage('Push image to ACR') {
            steps {
                script {
                    docker.withRegistry("http://${registryUrl}", registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning up docker residue...'
            sh 'docker system prune -f'
        }
    }
}
