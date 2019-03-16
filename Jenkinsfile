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

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }
        stage ('sonarqube'){
            environment {
                scanerHome = tool 'sonarqubescanner'
            }
            steps {
                WithSonarQubeEnv ('sonarqube'){
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout (time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
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
