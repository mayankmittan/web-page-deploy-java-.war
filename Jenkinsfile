pipeline {

agent any

tools {

maven 'My_Maven'

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



}

}
