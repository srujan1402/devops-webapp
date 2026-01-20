pipeline {
    agent any

    environment {
        APP_NAME = "devops-webapp"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build -t %APP_NAME%:%IMAGE_TAG% .
                docker tag %APP_NAME%:%IMAGE_TAG% %APP_NAME%:latest
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                bat '''
                docker-compose down
                docker-compose up -d
                '''
            }
        }
    }
}
