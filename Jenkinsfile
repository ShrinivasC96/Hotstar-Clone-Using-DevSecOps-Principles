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
    }
}
