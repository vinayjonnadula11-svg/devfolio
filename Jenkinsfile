
pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\jonna\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
        DOCKERHUB_USER = 'vinay0650'
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

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_TOKEN'
                )]) {
                    bat 'echo %DOCKER_TOKEN% | "%DOCKER%" login -u %DOCKER_USER% --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat '"%DOCKER%" tag devfolio:%BUILD_NUMBER% %DOCKERHUB_USER%/devfolio:%BUILD_NUMBER%'
                bat '"%DOCKER%" tag devfolio:%BUILD_NUMBER% %DOCKERHUB_USER%/devfolio:latest'
                bat '"%DOCKER%" push %DOCKERHUB_USER%/devfolio:%BUILD_NUMBER%'
                bat '"%DOCKER%" push %DOCKERHUB_USER%/devfolio:latest'
            }
        }
    }
}
