pipeline {
    agent { label 'slave1' }
    stages {
        stage('chechkout') {
            steps {
                sh 'git clone https://github.com/REUsha007/hello-world-war'
            }
        }
         stage('build') {
            steps {
                sh 'mvn package'
            }
        }
             }
}
