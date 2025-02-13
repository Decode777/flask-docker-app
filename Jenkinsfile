// Jenkinsfile
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
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").run('-p 5000:5000 --name flask-app')
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    bat 'docker stop flask-app || true'
                    bat 'docker rm flask-app || true'
                }
            }
        }
    }
}