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
    REGISTRY = "us.gcr:tttttt"
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
     branch 'dev'
        
    }
    steps {
        script {
          app = docker.build(REGISTRY)
            }
    
    }
    stage("Push to Registry"){
    when {
                branch 'dev'
            }
    }
    steps {
          script {
              docker.withRegistry('us.gcr:tttttt', 'harbor') {
              app.push("${env.BUILD_NUMBER}")
                app.push("latest")
                    }
                }
       }

    stage("Deploy to RedHat Openshift"){
    // Do Something
    }
    stage("Check"){
    // Do Something
    }
}
}