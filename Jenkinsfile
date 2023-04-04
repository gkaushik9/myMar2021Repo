pipeline {
    agent any

    environment {
     tomcat_url = 'http://ec2-3.138-244-28.us.east-2.compute.amazonaws.com:8080/'
    }
  
    tools {
     maven 'Maven3'
    }

    stages {
        stage('slack notify b4 start') {
            steps {
              echo "Started build just now"
                 slackSend  channel: 'feb-2021-weekend-batch', message: 'Build just started'
              }
        }

        stage ('checkout') {
           steps {
             checkout([$class: 'GITSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '
           }
        }

        stage ('Build') {
            steps {
                sh 'mvn clean install -f MyWebApp/pom.xml'
            }
        }

        stage ('JaCoCo') {
          steps {
            jacoco()
          }
        }

        stage ('Slack Notification') {
          steps {
               echo "deployed to Dev Env successfully"
                  slackSend  channel: 'feb-2021-weekend-batch', message: 'DEV Deployement was successful'
          }
        }
    }
}
