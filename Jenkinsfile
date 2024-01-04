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
        sh "docker --version"
        sh "docker-compose --version"
        sh "docker-compose -f docker-compose.yml up -d "
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
