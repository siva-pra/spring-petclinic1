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
               
                git branch: 'declerative', credentialsId: 'MAVEN_NODE', url: 'https://github.com/siva-pra/spring-petclinic1.git' 
            }
        }
        stage('Build') {
            steps {
                 withSonarQubeEnv(installationName:'SONAR_9.5.4', envOnly: true, credentialsId:'SONAR_TOKEN'){
                     sh "mvn package sonar:sonar"
                    
                 }
            }
        }
       
    
    }
   
}