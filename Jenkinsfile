pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-app .'
            }
        }

        stage('Tag Image') {
            steps {
                bat 'docker tag my-app ghcr.io/naveen4-code/my-app:latest'
            }
        }

        stage('Login to GHCR') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'ghcr-credentials',
                    usernameVariable: 'GHCR_USER',
                    passwordVariable: 'GHCR_TOKEN'
                )]) {
                    bat 'echo %GHCR_TOKEN% | docker login ghcr.io -u %GHCR_USER% --password-stdin'
                }
            }
        }

        stage('Push to GHCR') {
            steps {
                bat 'docker push ghcr.io/naveen4-code/my-app:latest'
            }
        }
    }
}