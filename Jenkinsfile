pipeline {
    tools{
        maven 'MAVEN_HOME'
    }
    triggers { 
            cron('*/30 * * * *')
            pollSCM('* * * * *')
    }

    agent { label 'maven' }
    stages {
        stage('SourceCode') {
            steps {
               
               git branch: 'declerative', credentialsId: 'JENKINS_BUILD', url: 'https://github.com/siva-pra/spring-petclinic1.git'
            }
        }
        stage('Build') {
            steps {
                 withSonarQubeEnv(installationName:'SONAR_9.5.4'){
                     sh "mvn package sonar:sonar"
                     echo "${env.SONAR_HOST_URL}"
                 }
            }
        }
       
    }
   
}