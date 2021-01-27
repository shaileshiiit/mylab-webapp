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
                        nexusUrl: '172.20.10.73:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'Release', 
                        version: "${version}"

                }
            }
        //Stage4 : Ansible play book
        stage ('Invoke playbook on the ansible controller'){
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansiblecontroller', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /opt/playbook/deploytotomcat.yaml -i /opt/playbook/hosts', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }   
       }  
    }