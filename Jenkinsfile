pipeline{

  agent any

  tools {
    maven 'maven3'
  }

  triggers{
    pollSCM('* * * * *')
  }
  stages {
    stage('1. Git'){
      steps {
        git branch: 'Declarative', changelog: false, poll: false, url: 'https://github.com/davbc/tomcat-webapp-war.git'
      }
    }

    stage('2. Maven'){
      steps{
        sh 'mvn clean package
      }
    }
  }
}
