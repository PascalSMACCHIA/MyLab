pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment {
      ArtifactId = readMavenPom().getArtifactId()
      Version = readMavenPom().getVersion()
      GroupId = readMavenPom().getGroupId()
      Name = readMavenPom().getName()
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
              nexusArtifactUploader artifacts:
               [[artifactId: "${ArtifactId}",
               classifier: '',
               file: 'target/VinayDevOpsLab-"${Version}".war',
               type: 'war']],
                credentialsId: 'a0195b63-e930-4369-a221-d18da7c9cd59',
                groupId: "${GroupId}",
                nexusUrl: '10.255.161.149:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'PascalDevOpsLab-SNAPSHOT',
                version: "${Version}"
            }
        }

        stage ('Print environment Variables'){
          steps {
            echo "Artifact Id is '${ArtifactId}'"
            echo "Version is '${Version}'"
            echo "GroupId is '${GroupId}'"
            echo "Name is '${Name}'"
          }
        }




    }

}
