pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t hotstar-clone .'
            }
        }

        stage('Security Scan - Trivy') {
            steps {
                sh 'trivy image hotstar-clone'
            }
        }
        stage('Docker Login) {
              steps {
                  withCredentials([usernamePassword(
                      credentialsId: 'dockerhub-cred',
                      usernameVariable: 'DOCKER_USER',
                      passwordVariable: 'DOCKER_PASS
                  )]) {
                      sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                  }
              }
        }
        stage('Push Image') {
            steps {
                sh 'docker tag hotstar-clone$DOCKER_USER/hotstar-clone:latest'
                sh 'docker push $DOCKER_USER/hotstar-clone:latest'
            }
        }
    }
}
