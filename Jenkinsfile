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
                    openshift.withCluster( 'https://c100-e.us-south.containers.cloud.ibm.com:32343', '4YH_kqNnpDx8bFj-ODEhDfzJbOw3xrsd7CSTtzyuNEY' ) {
                        openshift.withProject( 'project-icbs' ) {
                        //echo "Hello from project ${openshift.project()} in cluster ${openshift.cluster()}"
                        openshift.apply('ace-openshift-deployment-bancamovil.yaml').object()
                        }
                    }
                }
            }
        }  
    }
}
