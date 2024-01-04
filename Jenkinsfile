pipeline {
  agent none

  environment {
    GIT = 'https://github.com/divija231/raow.git'
    BRANCH = 'master'
    DOCKER_HUB_REPO = 'your-docker-hub-username/your-repo-name'
  }

  stages {
    stage("Cloning from Git") {
      agent { 
        label 'jenkins'
      }
      steps {
        script {
          checkout([$class: 'GitSCM', branches: [[name: BRANCH]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: GIT]]])
          sh "ls"
          sh "docker --version"
          sh "docker-compose --version"
          sh "docker-compose -f docker-compose.yml up -d"
          sh "ls"
          sh "docker ps -aq"
          sh "docker images"
        }
      }
    }

    stage("Checking") {
      agent any 
      steps {
        sh "docker images"
      }
    }

    stage("Pushing to Docker Hub") {
      agent {
        label 'jenkins'
      }
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPass', usernameVariable: 'divi')]) {
          script {
            // Log in to Docker Hub
            sh "docker login -u ${env.divi} -p ${env.dockerHubPass}"

            // Tag the image for Docker Hub
            sh "docker tag centos1:latest ${DOCKER_HUB_REPO}:latest"

            // Push the image to Docker Hub
            sh "docker push ${DOCKER_HUB_REPO}:latest"
          }
        }
      }
    }
  }
}
