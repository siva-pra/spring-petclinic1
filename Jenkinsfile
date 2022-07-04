pipeline {
    agent { label 'maven' }
    triggers { 
        cron('45 23 * * 1-5')
        pollSCM('*/5 * * * *')
    }
	tools {
		maven 'MAVEN_HOME'
	}
    stages {
        stage('scm') {
            steps {
               
                git branch: 'declarative', credentialsId: 'JENKINS_BUILD', url: 'https://github.com/siva-pra/spring-petclinic1.git'
            }
        }
        stage('build') {
            steps {
                withSonarQubeEnv(installationName: 'SONAR_9.5.4') {
                    sh "mvn clean package sonar:sonar"                                  
                }
            }
        }
		stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}