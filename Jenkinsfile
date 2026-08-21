pipeline {
    agent any

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
                bat 'docker build -t my-static-site .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo 'Stopping old container...'
                bat 'docker stop my-static-site-container || exit /b 0'
                bat 'docker rm my-static-site-container || exit /b 0'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Starting Docker container...'
                bat 'docker run -d --name my-static-site-container -p 8080:80 my-static-site'
            }
        }

        stage('Check Container') {
            steps {
                echo 'Checking Docker container...'
                bat 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
            echo 'Website: http://localhost:8080'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}