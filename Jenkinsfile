pipeline {
    agent any
    
    stages {
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat Deploy Dev') {
            steps {
                sshagent(['TomcatDev']){
                sh "scp -o StrictHostKeyChecking=no target/hr-api.war ec2-user@172.31.1.21:/opt/sammu/webapps/"
                sh "ssh ec2-user@172.31.1.21 /opt/sammu/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.1.21 /opt/sammu/bin/startup.sh"
            }
            }
        }
    }
    post {
  always {
    cleanWs()
  }
}
}
