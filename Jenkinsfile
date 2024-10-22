pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'
        DOCKER_IMAGE_NAME = 'oussachour/hello-world-app:latest' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/AchourOussama/hello-world-python', branch: 'main' 
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build("${DOCKER_IMAGE_NAME}") 
                }
                
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        app.push("latest")  
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
