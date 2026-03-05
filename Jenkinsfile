pipeline {
  agent any
  stages {
    stage('checkout code'){
        steps {
          checkout scm
        }
    }
    stage('Build Docker Image') {
            steps {
                sh 'docker build -t hotstar-clone .'
            }
        }
  }
}
