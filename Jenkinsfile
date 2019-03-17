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

     stage ('sonarqube'){
         def mvnHome = tool name: 'maven-3', type: 'maven'
                withSonarQubeEnv ('sonarqube'){
                    sh "${mvnHome}/bin/mvn sonar:sonar"
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
