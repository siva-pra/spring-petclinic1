pipeline{
    agent  { node { label 'maven' } }
    stages{
        stage('git repo'){
            steps{
                git branch: 'master', credentialsId: 'MAVEN_NODE', url: 'https://github.com/spring-projects/spring-petclinic1.git'
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
