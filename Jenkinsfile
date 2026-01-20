pipeline {
    agent any

    environment {
        APP_NAME = "devops-webapp"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/srujan1402/devops-webapp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                docker build -t $APP_NAME:$IMAGE_TAG .
                docker tag $APP_NAME:$IMAGE_TAG $APP_NAME:latest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker-compose down
                docker-compose up -d
                '''
            }
        }
    }
}
