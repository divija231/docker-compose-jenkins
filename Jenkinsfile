pipeline{
  agent none
  environment{
    GIT = 'https://github.com/divija231/raow.git'
    BRANCH ='master'
    
  }
  stages{
    stage("removing docker iamges and containers"){
      agent{ 
          label 'jenkins'
      }
      steps{
        sh "docker ps"
        sh "docker images"
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
        sh "docker tag nginx divija231/minewithdockeryaml1:latest"
        sh "docker push divija231/minewithdockeryaml1:latest"
        }
      }

    }
    
  }
}

