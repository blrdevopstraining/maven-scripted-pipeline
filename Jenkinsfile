node ("rhel-node"){
    def mvn_version = 'maven3.8.4'

    stage('clone') { // for display purposes
        git 'https://github.com/daticahealth/java-tomcat-maven-example.git'
    }
    stage('Build') {

            if (isUnix()) {
                    withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) {
                    sh '"mvn" -Dmaven.test.failure.ignore clean package'
                    }
                
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
    }
}
