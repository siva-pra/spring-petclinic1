pipeline{
    agent  any
    stages{
        stage('git repo'){
            steps{
               git credentialsId: 'MAVEN_NODE', url: 'https://github.com/siva-pra/spring-petclinic1.git'
             }
        }
        stage('build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('junit test report'){
            steps{
                junit '**/TEST-*.xml'
            }
        }
        stage('archive artifacts'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
    }
}
