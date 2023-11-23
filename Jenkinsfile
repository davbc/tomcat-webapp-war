node {

  def mvnHome = tool name: "maven3"

  properties ([pipelineTriggers([pollSCM('* * * * *')]) ])
  
  stage('1. clone code') {
    echo "cloning source code"
    git branch: 'script', url: 'https://github.com/davbc/tomcat-webapp-war.git'
  }
  stage('2. maven build'){
    echo "building code now"
    sh "${mvnHome}/bin/mvn clean package"    
  }
  stage('3. sonarqube'){
    echo "code quality scan"
    sh "${mvnHome}/bin/mvn sonar:sonar"
  }
  stage('4. Nexus'){
    echo "Nexus Artifactory"
    sh "${mvnHome}/bin/mvn deploy"
  }
  stage('5. Deploy'){
    echo "deploy to tomcat"
    deploy adapters: [tomcat9(path: '', url: 'http://54.209.168.21:8080/')], contextPath: null, onFailure: false, war: 'target/*war'
  }
}
