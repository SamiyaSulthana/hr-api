@Library('jhc') _
pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
             echo "${params.ParamaterizedExecution}"
             git branch: "${params.ParamaterizedExecution}", credentialsId: 'GitKey', url: 'https://github.com/SamiyaSulthana/hr-api'
            }
        }
        stage('Maven Build') {
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
