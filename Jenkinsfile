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
              script {

              def NexusRepo = Version.endsWith("SNAPSHOT") ? "PascalDevOpsLab-SNAPSHOT" : "PascalDevOpsLab-Release"

              nexusArtifactUploader artifacts:
                [[artifactId: "${ArtifactId}",
                classifier: '',
                file: "target/${ArtifactId}-${Version}.war",
                type: 'war']],
                credentialsId: 'a0195b63-e930-4369-a221-d18da7c9cd59',
                groupId: "${GroupId}",
                nexusUrl: '10.255.161.149:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: "${NexusRepo}",
                version: "${Version}"

              }
            }
        }

        // Stage 4 : Print some information

        stage ('Print environment Variables'){
          steps {
            echo "Artifact Id is '${ArtifactId}'"
            echo "Version is '${Version}'"
            echo "GroupId is '${GroupId}'"
            echo "Name is '${Name}'"
          }
        }

        // stage 5 : Deploying the build artifact to apache Tomcat



        stage ('Remote SSH'){
          steps {
          scripts {


          def remote = [:]
          remote.name = "tomcat"
          remote.host = "10.255.161.226"
          remote.user = 'ansibleadmin'
          remote.password = 'ansibleansible'
          remote.allowAnyHosts = true

          
                echo "Deploying the file war on Tomcat servers ..."
                sshCommand( remote: remote, command: ansible-playbook /opt/ansible/downloadanddeploy.yaml -i /opt/ansible/hosts)

                }
              }

          }


    }

}
