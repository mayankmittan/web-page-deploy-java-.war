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
  stage('Sonar Analysis') {
environment {
SCANNER_HOME = tool 'my_sonar'
PROJECT_NAME = "my_sonar"
  mvn sonar:sonar \
  -Dsonar.projectKey=my_sonar \
 
  -Dsonar.login=ebf5abda01c49688c5ae0c981f7085a09b850360
}
  }
steps {
withSonarQubeEnv('crediantialsId: 'jenkins-mm', installationName: 'my_sonar') {
sh '/root/opt/sonarscanner' \
                  -Dsonar.host.url=http://18.222.117.40:9000 \
-Dsonar.java.binaries=build/classes/java/ \
-Dsonar.projectKey=$PROJECT_NAME \
-Dsonar.sources=.'''
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
