pipeline {
    agent any
    environment {
        registry = "80190363/ibmace"
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
                    docker.withRegistry( '', 'dockerhub' ) {
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
                        sh 'oc apply -f /var/lib/jenkins/workspace/nnectEnterprise-Openshift_masterace-openshift-deployment-bancamovil.yaml'
                        }  
                }
            }
        }  
}
