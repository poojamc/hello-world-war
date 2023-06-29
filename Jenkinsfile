pipeline {
  agent any
  
  stages {
    stage('checkout') {
       steps {
         sh 'rm -rf *'
         sh 'rm -rf hello-world-war'
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
      
         sh 'cp /var/lib/jenkins/workspace/demo-jfrog/hello-world-war/target/hello-world-war-1.0.0.war /opt/apache-tomcat-8.5.90/webapps'
       }
    }
  }
}
