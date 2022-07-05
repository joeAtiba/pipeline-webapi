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
                    dockerImage = docker.build(registryName, dockerFilePath)
                    //dockerImage = docker.build('./webapi/')
               }
            }
        }
    }
}
