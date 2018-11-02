pipeline {
    agent { label 'centos' }
    stages {
        stage ('Checkout') {
          steps {
            git 'https://github.com/vedhamurthy/spring-petclinic.git'
          }
        }
        stage('Build') {
             agent { docker 'maven:3.5-alpine' }
             steps {
                sh 'mvn clean package'
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
             }
        }
        stage('Deploy') {
          steps {
            input 'Do you approve the deployment?'
            sh 'scp target/*.jar user@vedlatha1113.mylabserver.com:/opt/pet/'
            sh "ssh user@vedlatha1113.mylabserver.com 'nohup java -jar /opt/pet/*jar &'"

          }
        }

	
     }
}
