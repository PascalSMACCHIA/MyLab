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
              nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.9.war', type: 'war']], credentialsId: 'a0195b63-e930-4369-a221-d18da7c9cd59', groupId: 'com.vinaydevopslab', nexusUrl: '10.255.161.149:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'PascalDevOpsLab-SNAPSHOT', version: '0.0.9'
            }
        }



    }

}
