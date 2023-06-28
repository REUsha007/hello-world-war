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
                sshagent(['da1618c9-da22-4258-a64f-f09c3b113004']) {
                sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/demojfrogpipeline/target/hello-world-war-1.0.3.war root@ip-172-31-9-146:/opt/apache-tomcat-8.5.90/webapps'
                        }
                   }
}
}
}
