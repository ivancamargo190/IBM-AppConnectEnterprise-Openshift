pipeline {
    agent any
    environment {
        registry = "miguelhalliburton/ibmer"
        registryCredential = 'dockerhub'
    }
    stages {
        
        stage('Build App Connect Enterprise Docker Image') {
            when { 
                branch 'master'
            }
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    
                }    
            }
        }
        
        stage('Push App Connect Enterprise Docker Image to Registry') {
            when {
                branch 'master'
            }
            steps {
                script {
                    docker.withRegistry( '', miguelhalliburton ) {
                        dockerImage.push()
                    }
                }
            }
        }
        
        stage('Deploy App Connect Enterprise Openshift Container Platform') {
            when {
                branch 'master'
            }
            steps {
                script {
                    sh "gcloud docker -- push DOCKER_IMAGE_NAME:latest"
                }
            }
        }    
    }
}
