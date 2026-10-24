
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Docker') {
            steps {
                bat '"C:\\Users\\jonna\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"C:\\Users\\jonna\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t devfolio:%BUILD_NUMBER% .'
            }
        }

        stage('Verify Docker Image') {
            steps {
                bat '"C:\\Users\\jonna\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" images devfolio'
            }
        }
    }
}
