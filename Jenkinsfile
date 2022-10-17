pipeline {
agent any
     environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "1192.168.48.0:8081"
        NEXUS_REPOSITORY = "nexus-repo"
        NEXUS_CREDENTIAL_ID = "nexus"
    }
    stages {
        

        stage ("Git checkout "){
            steps{
        git branch: 'main', 
            url: 'https://github.com/WassimBA/test.git'
            }
        
        }
    
        
                stage("Build & test Project") {
            steps {
                echo "Build & test Project"
                sh 'mvn clean package -DskipTests=true'
            }
        }
        

            stage("Sonar Test") {
            steps {
           
             sh 'mvn sonar:sonar -Dsonar.projectKey=a -Dsonar.host.url=http://192.168.48.0:9000 -Dsonar.login=d6a5b4ab1830302b9a63e1e90cca5809d993af8b'         
                 
               

            }
        }
           stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        
    
    
    }

}
