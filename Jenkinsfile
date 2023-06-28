pipeline{
  geant any
  stages {
    stage('checkout') {
       steps {
         sh 'git clone'
       }
    }
      stage('build') {
       steps {
         sh 'echo building the code'
       }
    }
      stage('Push artifacts into artifactory') { 
        steps { 
          rtUpload ( 
            serverId: 'my-artifactory', 
            spec: '''{ 
            "files": [ { 
            "pattern": "*.war", 
            "target": "example-repo-local/"
            } 
            ] 
            }'''
          )	
        }	}
  }
}
