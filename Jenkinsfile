pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'laravel-app-2'
    }
    
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/farisRajendra/hamdualah.git'
            }
        }
        
        stage('Setup Laravel') {
            steps {
                sh 'cp .env.example .env || true'
                sh 'touch database/database.sqlite || true'
                sh 'chmod -R 777 storage bootstrap/cache || true'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        
        stage('Run Docker Container') {
            steps {
                sh 'docker rm -f laravel-container-2 || true'
                sh 'docker run -d -p 8001:8000 --name laravel-container-2 -v "$(pwd):/var/www" $DOCKER_IMAGE'
            }
        }
        
        stage('Check Container') {
            steps {
                sh 'docker ps | grep laravel-container-2'
                sh 'docker logs laravel-container-2'
            }
        }
    }
}