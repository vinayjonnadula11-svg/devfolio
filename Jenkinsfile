
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
            }
        }

        stage('Verify Docker Image') {
            steps {
                bat '"%DOCKER%" images devfolio'
            }
        }
    }
}
