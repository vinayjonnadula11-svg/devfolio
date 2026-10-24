
pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\jonna\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Docker') {
            steps {
                bat '"%DOCKER%" version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"%DOCKER%" build -t devfolio:%BUILD_NUMBER% .'
                bat '"%DOCKER%" tag devfolio:%BUILD_NUMBER% devfolio:latest'
            }
        }

        stage('Verify Docker Image') {
            steps {
                bat '"%DOCKER%" images devfolio'
            }
        }

        stage('Deploy with Nginx') {
            steps {
                bat '"%DOCKER%" rm -f devfolio'
                bat '"%DOCKER%" run -d --name devfolio -p 8082:80 --restart unless-stopped devfolio:latest'
            }
        }
    }
}
