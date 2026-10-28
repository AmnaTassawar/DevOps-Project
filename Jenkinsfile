pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                echo 'Pulling code from GitHub repository...'
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                echo 'Running build and test steps for Task 3...'
                sh 'echo "Hello from Jenkins Pipeline!"'
                sh 'node -v || echo "Node check"'
                sh 'docker --version || echo "Docker check"'
            }
        }
    }
}
