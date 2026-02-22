pipeline {
    agent any

    environment {
        IMAGE_NAME = "fiber-app"
    }

    stages {
         stage('checkout') {
            steps {
                git 'https://github.com/myomin313/go-docker-pipeline.git'
            }
         }

         stage('Build Docker Image'){
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
         }

         stage('Run Tests'){
            steps {
                bat 'go test ./...'
            }
         }

         stage('Deploy') {
             steps {
                 bat 'docker compose down --remove-orphans'
                 bat 'docker rm -f fiber_app || exit 0'
                 bat 'docker rm -f fiber_db || exit 0'
                 bat 'docker compose up -d --build'
             }
         }

    }
}