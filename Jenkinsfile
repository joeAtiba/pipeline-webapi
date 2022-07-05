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
        
        stage('Debugging') {
            steps {
                echo 'Here is JENKINS_HOME:'
                echo "${JENKINS_HOME}"
            }
        }
        
        stage ('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build registryName dockerFilePath
                    //dockerImage = docker.build('./webapi/')
               }
            }
        }
    }
}
