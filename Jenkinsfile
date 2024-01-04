pipeline{
  agent none
  environment{
    GIT = 'https://github.com/divija231/raow.git'
    BRANCH ='master'
    
  }
  stages{
    stage("cremoving docker iamges and containers"){
      agent{ 
          label 'jenkins'
      }
      steps{
        sh 'docker stop $(docker ps -aq)'
        sh 'docker rm $(docker ps -aq)'
        sh 'docker rmi $(docker images)'
        sh 'docker images '
      }
    }
    stage("clonning from git"){
      agent{ 
          label 'jenkins'
      }
      steps{
        sh "ls"
        git url : GIT , branch : BRANCH
        sh "docker --version"
        sh "docker-compose --version"
        sh "docker-compose -f docker-compose.yml up -d "
        sh "ls "
        sh "docker ps -q"
        sh "docker images"
      }
    }  
    stage("checking"){
      agent any 
      steps{
        sh "docker images"
      }
    }
    stage("pushing into docker hub"){
      agent{
        label 'jenkins'
      }
      steps {
      withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPass', usernameVariable: 'divi')]){
        sh "docker login -u ${env.divi} -p ${env.dockerHubPass}"
        sh "docker tag nginx divija231/minewithdockeryaml:latest"
        sh "docker push divija231/minewithdockeryaml:latest"
        }
      }

    }
    
  }
}

