pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = '55420/devops-app'
        CREDENTIALS_ID = 'docker-hub-cred'
    }

    stages {
        stage('Stage 1: Pull code from GitHub') {
            steps {
                echo 'Pulling source code from GitHub...'
                checkout scm
            }
        }
        
        stage('Stage 2: Build Docker image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${DOCKER_IMAGE}:latest ."
            }
        }
        
        stage('Stage 3: Push image to Docker Hub') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                withCredentials([usernamePassword(credentialsId: "${CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo '$DOCKER_PASS' | docker login -u '$DOCKER_USER' --password-stdin"
                    sh "docker push ${DOCKER_IMAGE}:latest"
                }
            }
        }
    }
    
    post {
        success {
            echo '🎉 Task 3 Pipeline executed successfully with Docker build and push!'
        }
        failure {
            echo '❌ Pipeline failed. Please check the logs.'
        }
    }
}
