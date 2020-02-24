pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "us.gcr.io/sincere-chariot-260312/acebancamovil110007v2"
    }
    stages {
        
        stage('Build App Connect Enteprise Docker Image') {
            when { 
                branch 'master'
            }
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    
                }    
            }
        }
        stage('Push ACE Docker Image to Registry') {
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
        stage('Deploy ACE over Openshift Container Platform Test') {
            when {
                branch 'master'
            }
            steps {
                
                    }
                }
            }
        }
        stage('Deploy ACE over Openshift Container Platform Production') {
            when {
                branch 'master'
            }
            steps {
                
                    }
                }
            }
        }
    }
}
