pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            when{
                branch = "develop"
            }
            steps {
                git branch: 'main', credentialsId: 'jenkinsgit', url: 'https://github.com/lokipalapani1/lms'
            }
        }
    stage('Maven Build') { 
        when{
                branch = "develop"
            }
            steps {
                sh 'mvn clean package'
           }
    }  
     stage('Dev Deploy') {
         when{
                branch = "develop"
            }
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
