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
        
        // Only you can prevent cruftification of your docker server...
        stage('Docker Cleansing') {
            steps {
                sh 'docker rm $(docker ps -a -q)'
                sh 'docker rmi $(docker images -q)'
            }
        }
        
        stage ('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build(registryName, dockerFilePath)
                    //dockerImage = docker.build('./webapi/')
               }
            }
        }
    }
}
