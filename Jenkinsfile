node {

  def mvnHome = tool name: "maven3"
  stage('1. clone code') {
    echo "cloning source code"
    git branch: 'script', url: 'https://github.com/davbc/tomcat-webapp-war.git'
  }
  stage('2. maven build'){
    echo "building code now"
    sh "${mvnHome}/bin/mvn clean package"    
  }
}
