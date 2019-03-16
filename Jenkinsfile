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
            environment {
                scanerHome = tool 'sonarqubescanner'
            }
            steps {
                withSonarQubeEnv ('sonarqube'){
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout (time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                    sh 'mvn sonar:sonar'
                }
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
