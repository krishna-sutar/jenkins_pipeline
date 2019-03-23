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
        stage('deploy to Tomcat') {
		steps {	     
		 sshagent(['tomcat-dev']) {
		     sh 'cp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.17.114:/usr/share/tomcat/webapps'
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
