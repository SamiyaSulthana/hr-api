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
             tomcatdeploy("ec2-user","172.31.1.21")
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
