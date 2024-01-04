pipeline{
  agent none
  environment{
    GIT = 'https://github.com/divija231/raow.git'
    BRANCH ='master'
    
  }
  stages{
    stage("clonning from git"){
      agent{ 
          label 'jenkins'
      }
      steps{
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
