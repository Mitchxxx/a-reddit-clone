pipeline {
	agent any
  tools {
    jdk 'jdk17'
    nodejs 'node16'     
  }
  environment {
    SCANNER_HOME = tool 'sonar-scanner'
    APP_NAME = 'reddit-clone-app'
    RELEASE = '1.0.0'
    DOCKER_USER = 'mitchxxx'
    DOCKER_PASS = 'docker'
    IMAGE_NAME = "${DOCKER_USER}" + "/" + "APP_NAME"
    IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
  }
  stages {
    stage('Clean Workspace') {
      steps {
        cleanWs()
      }
    }
   stage('Checkout from Git') {
      steps {
        git branch: 'main', url ''
    }
  }
}
