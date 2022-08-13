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
        stage ('scm') {
            steps {
                git branch: 'jfrog', url: 'https://github.com/siva-pra/spring-petclinic1.git'
            }
        }
        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "JFROG_OSS",
                    releaseRepo: "siva-maven-releases",
                    snapshotRepo: "siva-maven-snapshots"
                )

               
            }
        }
        stage ('Exec Maven') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'JFROG_OSS', usernameVariable: 'ARTIFACTORY_USERNAME', passwordVariable: 'ARTIFACTORY_PASSWORD')]) {
                    rtMavenRun (
                        tool: 'MAVEN_HOME', // Tool name from Jenkins configuration
                        pom: 'pom.xml',
                        goals: 'clean install ',
                        deployerId: "MAVEN_DEPLOYER"
                    )
                }
            }
        }
         stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: 'JFROG_OSS'
                )
            }
        }
    }
}