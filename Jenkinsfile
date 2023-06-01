pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'jenkins', git url: 'https://github.com/lokipalapani1/lms'
            }
        }
    stage('Maven Build') {
            steps {
                sh 'mvn clean package'
           }
    }  
     stage('Dev Deploy') {
            steps {
                sshagent(['tomcat-dev']) {
                    sh "scp -o StrictHostKeyChecking=no target/lms.war ec2-user@172.31.22.194:/opt/tomcat9/webapps/"
                    sh "ssh ec2-user@172.31.22.194 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.22.194 /opt/tomcat9/bin/startup.sh"
        }
        
        
    }
     
}
}
}
