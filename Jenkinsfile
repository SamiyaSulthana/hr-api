pipeline {
    agent any

    stages {
        stage('Git Checkout') {
//             when{
//                 expression{
//                     params.ParamaterizedExecution == "develop"
//                 }
//             }
            steps {
//                 echo "${params.ParamaterizedExecution}"
             git branch: "${params.ParamaterizedExecution}", credentialsId: 'GitKey', url: 'https://github.com/SamiyaSulthana/hr-api'
            }
        }
        stage('Maven Build') {
//            when{
//                 expression{
//                     params.ParamaterizedExecution == "develop"
//                 }
//             }
            steps {
             sh 'mvn clean package'
            }
        }
         stage('Tomcat Deploy Dev') {
            steps {
             sshagent(['TomcatDev']) {
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
}
