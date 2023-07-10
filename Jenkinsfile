pipeline {
    agent any
    stages {
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
         stage('Tomcat Deploy') {
            steps {
                sshagent(['ssh-agent']) {
                sh "scp -o StrictHostKeyChecking=no target/hr-api.war ec2-user@172.31.34.221:/opt/tomcat9/webapps"
                sh "ssh ec2-user@172.31.34.221 /opt/tomcat9/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.34.221 /opt/tomcat9/bin/startup.sh"
            }
         }
    }
    }
}
