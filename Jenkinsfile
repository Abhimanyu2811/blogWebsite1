pipeline {
    agent any

    environment {
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
                    bat "docker build -t %IMAGE_NAME%:%IMAGE_TAG% ."
                }
            }
        }

        stage('Push Docker Image Locally') {
            steps {
                echo 'Docker image built and available locally. No push to ACR.'
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
