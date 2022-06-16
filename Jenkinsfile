pipeline {
    tools{
        maven 'MAVEN_HOME'
    }
    triggers { 
            cron('*/30 * * * *')
            pollSCM('* * * * *')
      }
      parameters {
           string(name: 'MVN-GOLE', defaultValue: 'package', description: 'this is build')
           choice(name: 'BRANCHS', choices: ['declerative', 'main'], description: 'Pick something')
            }
    agent { label 'maven' }
    stages {
        stage('SourceCode') {
            steps {
                git branch: "${params.BRANCHS}", credentialsId: 'MAVEN_NODE', url: 'https://github.com/siva-pra/spring-petclinic1.git', 
            }
        }
        stage('Build') {
            steps {
                sh "${params.MVN-GOLE}"
            }
        }
        stage('Test Results') {
            steps {
               junit '**/surefire-reports/*.xml'
            }
        }
        stage('Archive'){
            steps{
              archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
    }
}