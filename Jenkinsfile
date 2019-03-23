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
		     sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@13.233.195.169:/usr/share/tomcat/webapps'
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
