pipeline {
    agent any
    tools {
	maven 'java_maven'
    }  
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',		    
		credentialsId: '94debc7e-4fbd-4317-b2f2-f5a7c8aefe8c',
			url: "https://github.com/ag-cloudtechner/java-tomcat-maven-example.git"    
	    }
	}	
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }		    
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }	    
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

	stage('Deploy') {
            steps {
                echo 'Deployment done'
            }
        }
  }
}
