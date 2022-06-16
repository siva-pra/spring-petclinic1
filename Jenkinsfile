pipeline {
    tools{
        maven 'MAVEN_HOME'
    }
    triggers { upstream(upstreamProjects: 'upstream', threshold: hudson.model.Result.SUCCESS) }
    agent { label 'maven' }
    stages {
        stage('SourceCode') {
            steps {
                git branch: 'declerative', credentialsId: 'MAVEN_NODE', url: 'https://github.com/siva-pra/spring-petclinic1.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Archive and Test Results') {
            steps {
               junit '**/surefire-reports/*.xml'
               archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
    }
}