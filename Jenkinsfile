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
    post{
        always{
            mail (to: 'tellagorlasivaprasad1996@gmail.com',
                 subject: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) success.",
                 body: "Please visit ${env.BUILD_URL} for further information.",
                  )
        }
    }
}