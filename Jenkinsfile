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
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }	    
        stage('Sonar Testing') {
            steps {

                withSonarQubeEnv('sonar1') {
                    sh "mvn sonar:sonar"
                }
            }
        timeout(time: 30, unit: 'SECONDS')
	                if ("${json.projectStatus.status}" == "ERROR") {
                            currentBuild.result = 'FAILURE'
                            error('Pipeline aborted due to quality gate failure.')
                    }    
	}   

	stage('Deploy') {
            steps {
		    sh 'cp /root/.jenkins/workspace/pipeline/target/*.war /opt/apache-tomcat-9.0.58/webapps/'
            }
        }
  }
}
