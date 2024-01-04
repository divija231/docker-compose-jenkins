pipeline{
  agent none
  environment{
    GIT = 'https://github.com/divija231/raow.git'
    BRANCH ='master'
    
  }
  stages{
    stage("clonning from git"){
      steps{
        node { 
          label 'jenkins'
        }
        sh "ls"
        git url : GIT , branch : BRANCH
        sh "docker-compose -f docker-compose.yaml up -d "
        sh "ls "
        sh "docker ps -aq"        
      }
    }
    stage("checking"){
      agent any 
      steps{
        sh "docker images"
      }
    }
  }
}
