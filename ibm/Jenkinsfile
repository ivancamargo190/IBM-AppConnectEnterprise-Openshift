pipeline {
    agent any
    environment {
        PATH = "/usr/local/go/bin:$PATH"
        DOCKER_IMAGE_NAME = "us.gcr.io/sincere-chariot-260312/ace11007mq9003saldosv1os"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Compiling Program'
                sh 'go test -v'
            }
        }
        stage('Build Docker Image') {
            when { 
                branch 'dev'
            }
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    app.withRun("-d -p 8181:8181") { c ->
                        sh 'curl localhost:8181'
                    }    
                }
            }
        }
        stage('Push Docker Image to IBM Container Registry') {
            when {
                branch 'dev'
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
        stage('Deploy ACE to Openshift') {
            when {
                branch 'dev'
            }
            steps {
                milestone(1)
                kubernetesDeploy(
                  credentialsType: 'KubeConfig',
                  kubeconfigId: 'kubeconfig',
                  kubeConfig: [path: '/var/lib/jenkins/ace-openshift/.kube/config'],
                  configs: 'ace-openshift-deployment.yaml',
                  enableConfigSubstitution: true
                ) 
            }
        }
        stage('Get Service IP') {
            when {
                branch 'master'
            }
            steps {
                //milestone(1)
                retry(10) {
                    withCredentials([usernamePassword(credentialsId: 'pks_client', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                        script {
                            //sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@$pks_client \"kubectl get all -l app=gocicd -o wide\""
                            def ip = sh (script: "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@$pks_client \"kubectl get svc gocicd --output=jsonpath={'.status.loadBalancer.ingress[].ip'}\"", returnStdout: true)
                            sh 'sleep 5'
                            echo "IP is ${ip}"
                            echo "URL is http://${ip}:8181"
                            try {
                             //echo sh(script: "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@$kube-master-ip ls -la", returnStdout: true)
                             //sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@$kube-master-ip \"/usr/bin/touch /tmp/jenkins\""
                            } catch (err) {
                             echo: 'caught error: $err'
                            }
                        }
                    }
                }
            }
        }
    }
}
