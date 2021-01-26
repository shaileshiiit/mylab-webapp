pipeline{
    //Directives
    agent any

    tools {
        maven 'maven'
    }

    environment {
        artifactId = readMavenPom().getArtifactId()
        version = readMavenPom().getVersion()
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish to Nexus
        stage ('Nexus'){
            steps {
                echo ' Publish to Nexus......'
                
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: "${artifactId}", 
                        classifier: '', 
                        file: "target/${artifactId}-${version}.war", 
                        type: 'war']], 
                        credentialsId: 'Nexus', 
                        groupId: 'com.vinaysdevopslab', 
                        nexusUrl: '172.20.10.140:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'SNAPSHOT', 
                        version: "${version}"

                }

            }
           
       }  
    }