pipeline {
    agent any
    
    environment {
        DOCKER_HUB_CREDENTIALS = 'docker_credentials'
        DOCKER_IMAGE_NAME = 'bsoundarya/jenkins_pipeline'
        DOCKER_IMAGE_TAG = "latest-${env.BUILD_NUMBER}"
        GIT_URL = 'https://github.com/Github20806/jenkins_docker.git'
    }
    
    stages {
         stage('Checkout') {
            steps {
                git url: "${GIT_URL}"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        sh "docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        sh "docker push ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                    }
                }
            }
        }
        stage('Clean Up Local Image') {
            steps {
                script {
                    sh "docker rmi ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                }
            }
        }
    }
}
