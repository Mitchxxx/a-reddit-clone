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
        git branch: 'main', url: 'https://github.com/Mitchxxx/a-reddit-clone.git'
    }
  }
  stage('Sonarqube Analysis') {
      steps {
        withSonarQubeEnv('SonarQube-server'){
	  sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Reddit-Clone-CI \
             -Dsonar.projectKey=Reddit-Clone-CI '''
	}
    }
  }
  stage('Quality Gate') {
      steps {
        script {
          waitForQualityGate abortPipeline: false, credentials: 'sonarqube-token'
        }
    }
  }
  stage('Install Dependencies') {
      steps {
        sh "npm install"
    }
  }
  stage('Trivy FS Scan') {
      steps {
        sh "trivy fs . > trivyfs.txt"
    }
  }
}
}
