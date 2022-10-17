pipeline {
agent any
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
                sh 'mvn install'
                sh 'mvn clean package -DskipTests=true'
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
