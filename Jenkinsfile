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
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.1.war', type: 'war']], credentialsId: '74440630-6752-4906-bde1-70b840ba2253', groupId: 'com.vinaysdevopslab', nexusUrl: '54.242.133.154:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'SNAPSHOT', version: '0.0.1'
            }
        }
    }
}