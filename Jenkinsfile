node ("aws-node"){
    def mvnHome
    stage('clone') { // for display purposes
        git 'https://github.com/devopsdesk/game-of-life.git'
    }
    stage('Build') {
            if (isUnix()) {
                sh '"mvn" -Dmaven.test.failure.ignore clean package'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
    }
    stage('Results') {
        junit 'gameoflife-core/target/surefire-reports/*.xml'
        
    }
}
