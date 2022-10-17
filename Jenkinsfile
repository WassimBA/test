pipeline {
agent any
    stages {
        

        stage ("Git checkout "){
            steps{
        git branch: 'wassim_branch', 
            url: 'https://github.com/WassimBA/test.git'
            }
        
        }
    
        
                stage("Build & test Project") {
            steps {
                echo "Build & test Project"
                sh 'mvn install -DskipTests=true'
            }
        }
        

            stage("Sonar Test") {
            steps {
                echo "Sonar is ready"
                sh 'mvn sonar:sonar'

            }
        }
           
        
    
    
    }

}
