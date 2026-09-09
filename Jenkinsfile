pipeline {
    agent any

    environment {
        IMAGE_NAME = "factorial-app"
        IMAGE_TAG  = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/shivendra534/factorial-.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Run Container') {
            steps {
                sh """
                  docker rm -f factorial-app || true
                  docker run -d --name factorial-app ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }

        stage('Show Output') {
            steps {
                sh "docker logs factorial-app"
            }
        }
    }

    post {
        always {
            sh "docker system prune -f"
        }
    }
}
