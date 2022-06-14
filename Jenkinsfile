pipeline {
    tools{
        maven 'MAVEN_HOME'
        jar 'JAVA_HOME'
    }
    agent { label 'maven' }
    triggers { pollSCM('* * * * *') }
    stages {
        stage('SourceCode') {
            steps {
              git credentialsId: 'MAVEN_NODE', url: 'https://github.com/siva-pra/spring-petclinic1.git'
            }

        stage('Archive and Test Results') {
            steps {
               junit '**/surefire-reports/*.xml'
               archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
    }
}
        
