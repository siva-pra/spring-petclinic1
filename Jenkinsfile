pipeline {
    agent { label 'maven' }
    triggers {
        cron('30 */4 * * 1-5')
        pollSCM('30 11 * * 1-5')
    }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['declarative', 'main'], description: 'To Build')
        string(name: 'MAVEN_GOAL', defaultValue: 'clean package', description: 'For Build')
    }
    stages {
        stage('get clone code') {
            steps {
                git branch: 'declarative', credentialsId: 'JENKINS_BUILD', url: 'https://github.com/siva-pra/spring-petclinic1.git' 
            }
        }
        stage('To Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Archive') {
            steps {
                // archive artifacts
                archive 'target/*.jar'
            }
        }
        stage('Publish Build Result') {
            steps {
                junit '**/TEST-*.xml'
            }
        }
        stage("build & SonarQube analysis") {
            steps {
                withSonarQubeEnv(installationName:'SONAR_9.5.4') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}        