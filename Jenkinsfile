pipeline {
    agent any 
    
    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                    
                }
            }
        }

     stage ('SonarQube Analysis'){
                withSonarQubeEnv ('sonarqube'){
                    sh 'mvn package sonar:sonar'
                }
     }
        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }
   
                    
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                    
                }
            }
        }
    }
}
