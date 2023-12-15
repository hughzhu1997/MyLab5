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

        // Stage 2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage 3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts:
                [[artifactId: 'VinayDevOpsLab', 
                classifier: '', 
                file: 'target/VinayDevOpsLab-0.0.3-SNAPSHOT.war', 
                type: 'war']], 
                credentialsId: '0a0bc6c8-f184-4d8e-9775-bcda7b4130b6', 
                groupId: 'com.vinaysdevopslab', 
                nexusUrl: '172.20.10.52:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'VinaysDevOpsLab-SNAPSHOT', 
                version: '0.0.3-SNAPSHOT'

            }
        }

        // Stage 4 : Print some information
        stage ('Print Environment variables'){
            steps {
                echo "Artifact Id is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupId is '${GroupId}'"
                echo "Name is '${Name}'"

            }
        }

        // Stage 5 : Deploying
        stage ('Deploy'){
            steps {
                echo 'Deployinging......'

            }
        }
        
        
    }

}