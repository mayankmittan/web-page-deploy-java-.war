pipeline {
    agent any
    tools {
	maven 'my_maven'
    }  
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',		    
		credentialsId: '60ed7899-a6ba-4aec-ae5f-d4ad9c5da302',
			url: "${urls}"    
	    }
	}	
        stage('Build') {
            steps {
                sh 'mvn clean install'
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
}
