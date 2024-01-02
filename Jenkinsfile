pipeline{

  agent any

  tools {
    maven 'maven3'
  }

  triggers{
    pollSCM('* * * * *')
  }
  stages {
    stage('1. Clone'){
      steps {
        git branch: 'Declarative', url: 'https://github.com/davbc/tomcat-webapp-war.git'
      }
    }

    stage('2. Maven'){
      steps{
        sh 'mvn clean package'
      }
    }

    stage('3. SonarQube'){
      steps{
        sh 'mvn sonar:sonar'
      }
    }
    stage('4. Nexus'){
      steps{
        sh 'mvn deploy'
      }
    }
    stage('5. Approve'){
      steps{
        timeout(time: 3, unit: 'DAYS') {
         input message: "please approve"  
        }
      }
    }
    stage('6. Deploy'){
      steps{
       sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible-server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /home/ansible/opt/tomcat/webapp.yaml  ', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/opt/tomcat', remoteDirectorySDF: false, removePrefix: 'target', sourceFiles: 'target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
      }
    }
  }
}
