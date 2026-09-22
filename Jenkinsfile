pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "mohiiittt/node-devops-app:v1"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mohiit541/node-devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t node-devops-app:v1 .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" tag node-devops-app:v1 %DOCKER_IMAGE%'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    bat '''
                        echo %DOCKER_PASSWORD% | "C:\\Users\\DELL\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" login -u %DOCKER_USERNAME% --password-stdin
                        "C:\\Users\\DELL\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" push %DOCKER_IMAGE%
                    '''
                }
            }
        }

        stage('Check Docker Image') {
            steps {
                bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" images node-devops-app'
            }
        }
    }

    post {
        success {
            echo 'Build and Docker Hub Push Successful!'
        }

        failure {
            echo 'Build Failed!'
        }
    }
}