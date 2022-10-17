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
               
             sh 'mvn sonar:sonar -Dsonar.projectKey=a -Dsonar.host.url=http://192.168.1.50:9000 -Dsonar.login=d6a5b4ab1830302b9a63e1e90cca5809d993af8b'

              
                 
               

            }
        }
           
        
    
    
    }

}
