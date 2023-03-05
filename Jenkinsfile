node {
    def mvn_version = 'Maven3'

    stage('clone') { // for display purposes
        git 'https://github.com/devopsdesk/java-web-app-docker.git'
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
    stage('Build Docker Image'){
        sh 'docker build -t blrdevopstraining/java-web-app .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
          sh "docker login -u blrdevopstraining -p ${Docker_Hub_Pwd}"
        }
        sh 'docker push blrdevopstraining/java-web-app'
     }
     
      stage('Run Docker Image In Dev Server'){
        
        def dockerRun = ' docker run  -d -p 8080:8080 --name java-web-app blrdevopstraining/java-web-app'
         
         sshagent(['DOCKER_SERVER']) {
          sh 'ssh -o StrictHostKeyChecking=no ec2-user@13.233.60.209 docker stop java-web-app || true'
          sh 'ssh  ubuntu@13.233.60.209 docker rm java-web-app || true'
          sh 'ssh  ubuntu@13.233.60.209 docker rmi -f  $(docker images -q) || true'
          sh "ssh  ubuntu@13.233.60.209 ${dockerRun}"
       }
       
    }
    
     
}
    
}
