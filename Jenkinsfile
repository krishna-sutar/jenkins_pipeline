pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'Localmaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'Localmaven') {
                    sh 'mvn test' 
                }
            }
        }
        stage('Get Approval'){
            input "deploy to QA"
        }
        any agent {
            
            stage ('deploy to A') {
        stage ('Deployment Stage')
            }
        }
            steps {
                withMaven(maven : 'Localmaven') {
                    sh 'mvn install'
                }
            }
        }
    }
}
