pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
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

        // Stage3 : Publish the source code to Sonarqube
        stage ('Publish'){
            steps {
               nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.9.war', type: 'war']], credentialsId: 'aa11c095-d82f-47e1-b037-d4843eec4419', groupId: 'com.vinaysdevopslab', nexusUrl: '10.255.161.149:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'PascalDevOpsLab-SNAPSHOT', version: '0.0.9'
               }
            }
        }



    }
