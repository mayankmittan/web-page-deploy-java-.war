pipeline {

agent any

tools {

maven 'my_maven'

}

stages {

stage('Git Checkout') {

steps {

git branch: 'main',

credentialsId:'b0965fcc-041a-49ba-ba0b-9fea1c28df2d',

url: 'https://github.com/mittanmayank/done.git'

sh 'echo Git Checkout complete'

}

}

stage('compile') {

steps {

sh 'mvn clean install'

sh 'echo compile completed'

}

}

stage('SonarQube analysis') { 
  steps { 
    script{ def scannerHome = tool 'my_sonar'; 
           withSonarQubeEnv('my_sonar') {
             sh "${tool("my_sonar")}/bin/sonar-scanner \ 
             -Dsonar.projectKey=my_sonar \ 
             -Dsonar.projectName=my_sonar"
           }
          }
  }



stage('Quality Gate') {
steps {
timeout(time: 1, unit: 'MINUTES') {
waitForQualityGate abortPipeline:true
}
}
}


stage('package') {

steps {

sh 'mvn package'

}

}

stage('Unit test') {

steps {

sh 'mvn test'

}

}
stage('Deployment') {

steps {

sh 'cp /root/.jenkins/workspace/done/target/*.war /opt/tomcat/webapps'

}

}

stage('installing webapp') {

steps {

sh '/opt/tomcat/bin/startup.sh'

}

}


}

}
