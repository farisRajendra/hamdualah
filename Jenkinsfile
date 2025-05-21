pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'laravel-app-2'
    }
    
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/farisRajendra/hamdualah.git'
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
                sh 'docker run -d -p 8001:8000 --name laravel-container-2 $DOCKER_IMAGE'
            }
        }
    }
}