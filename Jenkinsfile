pipeline {
    tools{
        maven 'MAVEN_HOME'
    }
    triggers { 
            cron('*/30 * * * *')
            pollSCM('* * * * *')
    }

    parameters {
           string(name: 'MVN_GOLE', defaultValue: 'package', description: 'this is build')
           choice(name: 'BRANCHS', choices: ['declerative', 'main'], description: 'Pick something')
            }
    agent { label 'maven' }
    stages {
        stage('SourceCode') {
            steps {
               
                git branch: "${params.BRANCHS}", credentialsId: 'MAVEN_NODE', url: 'https://github.com/siva-pra/spring-petclinic1.git' 
            }
        }
        stage('Build') {
            steps {
                 sh "mvn ${params.MVN_GOLE}"
                 withSonarQubeEnv(installationName:'SONAR_9.5.4', envOnly: True, credentialsId:'SONAR_TOKEN'){
                     sh 'mvn package sonar:sonar'
                    
                 }
            }
        }
       
    
    }
   
}