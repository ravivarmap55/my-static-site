pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }

        stage('Test Docker') {
            steps {
                echo 'Testing Docker...'
                bat 'where docker'
                bat 'docker --version'
                bat 'docker ps'
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
                echo 'Running Docker container...'
                bat 'docker run -d --name my-static-site-container -p 8080:80 my-static-site'
            }
        }

        stage('Check Container') {
            steps {
                echo 'Checking container...'
                bat 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
            echo 'Open: http://localhost:8080'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}
