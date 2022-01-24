pipeline {
    agent any
    tools {
	maven 'my_maven'
    }  
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',		    
		credentialsId: '94debc7e-4fbd-4317-b2f2-f5a7c8aefe8c',
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
