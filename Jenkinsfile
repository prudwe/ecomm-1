pipeline {
    agent any
    
    environment {
        // Define environment variables for Docker Hub credentials
        DOCKER_HUB_USERNAME = credentials('dockerhub-username')
        DOCKER_HUB_PASSWORD = credentials('dockerhub-password')
        DOCKER_IMAGE_NAME = 'prudwe/test-pipeline' // Replace with your Docker Hub username and image name
        DOCKER_IMAGE_TAG = 'latest' // You can set a specific tag here
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", "-f Dockerfile .")
                }
            }
        }
        
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub
                    docker.withRegistry('https://hub.docker.com/', DOCKER_HUB_USERNAME, DOCKER_HUB_PASSWORD) {
                        // Push Docker image to Docker Hub
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}

