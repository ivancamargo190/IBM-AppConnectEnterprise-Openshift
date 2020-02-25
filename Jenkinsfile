pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "us.gcr.io/sincere-chariot-260312/acebancamovil110007v2"
    }
    stages {
        
        stage('Build App Connect Enterprise Docker Image') {
            when { 
                branch 'master'
            }
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    
                }    
            }
        }
        stage('Push App Connect Enterprise Docker Image to Registry') {
            when {
                branch 'master'
            }
            steps {
                script {
                     docker.withRegistry('https://us.gcr.io', 'gcr') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    
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
