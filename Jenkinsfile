pipeline {
    /* insert Declarative Pipeline here */
    agent any 

    tools {
  // No valid tools specified
    maven 'maven'
    }

    stages {
        stage ("Build") {
            steps {
                echo "This is build stage to create maven artifacts"
                sh 'mvn clean install package'

            }
        }

    stage ("Test") {
            steps {
                echo "This is testing stage"
            }
        }
    stage ("Publish Artifacts to Nexus") {
            steps {
                echo "This is publishing build artifcats to Nexus"
                nexusArtifactUploader artifacts:
                [[
                    artifactId: 'VinayDevOpsLab', 
                    classifier: '', 
                    file: 'target/VinayDevOpsLab-0.0.1.war', 
                    type: 'war']], 

                    credentialsId: 'Nexus', 
                    groupId: 'com.vinaysdevopslab', 
                    nexusUrl: '172.20.10.73:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'SNAPSHOT', 
                    version: '0.0.1'
            }
        }
    }
}