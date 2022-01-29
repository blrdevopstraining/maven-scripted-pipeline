node ("rhel-node"){
    def mvnHome
    stage('clone') { // for display purposes
        git 'https://github.com/daticahealth/java-tomcat-maven-example.git'
    }
    stage('Build') {
            if (isUnix()) {
                sh '"mvn" -Dmaven.test.failure.ignore clean package'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
    }
}
