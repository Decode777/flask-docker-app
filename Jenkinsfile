pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "flask-docker-app"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Decode777/flask-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t %DOCKER_IMAGE%:%DOCKER_TAG% ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat "docker run -d -p 5000:5000 --name flask-app %DOCKER_IMAGE%:%DOCKER_TAG%"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    bat 'docker stop flask-app || echo "Container already stopped"'
                    bat 'docker rm flask-app || echo "Container already removed"'
                }
            }
        }
    }
}