pipeline {
    agent any

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

        stage('Check Docker Image') {
            steps {
                bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" images node-devops-app'
            }
        }
    }

    post {
        success {
            echo 'Build Successful!'
        }

        failure {
            echo 'Build Failed!'
        }
    }
}