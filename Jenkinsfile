pipeline {
  agent any
  
  stages {
    stage('checkout') {
       steps {
         sh 'rm -rf *'
         sh 'git clone https://github.com/poojamc/hello-world-war.git'
       }
    }
      stage('build') {
       steps {
         sh 'mvn package'
       }
    }
      stage('Push artifacts into artifactory') { 
        steps { 
          rtUpload ( 
            serverId: 'my-artifactory', 
            spec: '''{ 
                "files": [ 
                    { 
                        "pattern": "*.war", 
                        "target": "example-repo-local/"
            } 
            ] 
            }'''
          )	
        }
      }
     stage('deploying war file to tomcat') {
       steps {
         sh 'rm -rf*'
         sh 'cp /var/lib/jenkins/workspace /opt/apache-tomcat-8.5.90/webapps'
       }
    }
  }
}
