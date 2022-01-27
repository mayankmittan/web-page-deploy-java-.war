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
        stage('Building') {
            steps {
                sh 'mvn clean install'
            }
        }		    
	    
        stage('Sonar Testing') {
            steps {

                withSonarQubeEnv('sonar1') {
                    sh "mvn sonar:sonar"
                }
            }
	}   
         stage('Quality Gate'){
		 steps{
            timeout(time: 30, unit: ‘SECONDS’) {
              def qg= waitForQualityGate()
            if (qg.status!= ‘OK’){
                error “Pipeline aborted due to quality gate failure: ${qg.status}”
            }
        }         
              echo ‘Quality Gate Passed’

    }
	 }
	    stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
	stage('Deploy') {
            steps {
		    sh 'cp /root/.jenkins/workspace/pipeline/target/*.war /opt/apache-tomcat-9.0.58/webapps/'
            }
        }
  }
}
