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

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'shrinivas2616',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker tag hotstar-clone shrinivas2616/hotstar-clone:latest'
                sh 'docker push shrinivas2616/hotstar-clone:latest'
            }
        }
        stage('Run Container') {
            steps {
                sh '''
                docker stop hotstar-container || true
                docker rm hotstar-container || true
                docker run -d -p 3000:80 --name hotstar-container shrinivas2616/hotstar-clone:latest
                '''
            }
        }

    }
}
