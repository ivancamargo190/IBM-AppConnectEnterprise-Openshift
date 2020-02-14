pipeline {
    agent {
      node {label 'App Connect Enterprise'}
    }
    environment {
    APPLICATION_NAME = 'App Connect Enterprise'
    GIT_REPO="https://github.com/ivancamargo190/IBM-AppConnectEnterprise-Openshift.git"
    GIT_BRANCH="dev"
    STAGE_TAG = "promoteToQA"
    DEV_PROJECT = "ace-openshift"
    STAGE_PROJECT = "ace-openshift"
    TEMPLATE_NAME = "App Connect Enterprise"
    ARTIFACT_FOLDER = "target"
    PORT = 8081;
}
stages {
    stage("Check SCM"){
    steps {
    git branch: "${GIT_BRANCH}", url: "${GIT_REPO}" // declared in environment
  }
    }
    stage("Build AppConnectEnterprise Image"){
   when {
        expression {
            openshift.withCluster() {
            openshift.withProject(DEV_PROJECT) {
                return !openshift.selector("bc", "${TEMPLATE_NAME}").exists();
                }
            }
        }
    }
    steps {
        script {
            openshift.withCluster() {
                openshift.withProject(DEV_PROJECT) {
                    openshift.newBuild("--name=${TEMPLATE_NAME}", "--docker-image=docker.io/nginx:mainline-alpine", "--binary=true")
                }
            }
        }
    }
    }
    stage("Push to Registry"){
    // Do Something
    }
    stage("Deploy to RedHat Openshift"){
    // Do Something
    }
    stage("Check"){
    // Do Something
    }
}
}