pipeline {
    agent any
    stages {
        stage('chechkout') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/REUsha007/hello-world-war.git'
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
                 serverId: 'myartifactory', 
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
        stage('deploy') {
            steps {
                sh 'scp /var/lib/jenkins/workspace/hello-world-war.war root@ip-172-31-29-215:/opt/apache-tomcat-8.5.90/webapps/'
                }
        }
    }
}
