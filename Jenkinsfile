pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'abhimanyu1234' // <-- change this to your Docker Hub username
        IMAGE_NAME = 'nodejsdocker1'
        IMAGE_TAG = 'latest'
        TF_WORKING_DIR = '.'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Abhimanyu2811/blogWebsite1.git'
            }
        }

        stage('Install Node.js Dependencies') {
            steps {
                dir('blogWebsite-main') {
                    bat 'npm install'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('blogWebsite-main') {
                    bat "docker build -t %DOCKER_HUB_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG% ."
                }
            }
        }

        stage('Docker Hub Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASS')]) {
                    bat "echo %DOCKERHUB_PASS% | docker login -u %DOCKERHUB_USER% --password-stdin"
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                bat "docker push %DOCKER_HUB_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG%"
            }
        }
    }

    post {
        success {
            echo 'All stages completed successfully!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
