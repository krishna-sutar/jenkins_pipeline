pipeline {
    agent { label 'mavenlabel' }

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
        
                
        stage ('Build on slave1') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    node('slave1') {
                    sh 'mvn package'
                    }
                }
            }
        }
        
        
        stage ('Building and Integrating Sonar') {

            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn package sonar:sonar'
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
