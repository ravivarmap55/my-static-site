pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-static-site'
        CONTAINER_NAME = 'my-static-site-container'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning GitHub repository...'

                git branch: 'main',
                    url: 'https://github.com/ravivarmap55/my-static-site.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'

                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo 'Stopping old container...'

                sh '''
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Starting new container...'

                sh '''
                    docker run -d \
                    --name ${CONTAINER_NAME} \
                    -p 8080:80 \
                    ${IMAGE_NAME}:latest
                '''
            }
        }

        stage('Check Container') {
            steps {
                echo 'Checking Docker container...'

                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}