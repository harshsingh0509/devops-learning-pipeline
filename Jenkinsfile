pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                credentialsId: 'github-credentials', 
                url: 'https://github.com/harshsingh0509/devops-learning-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build & Push') {
            steps {
                sh 'echo $DOCKER_CREDENTIALS | docker login --username harshsinngh --password-stdin'
                sh 'docker build -t harshsinngh/devops-learning-app:latest .'
                sh 'docker push harshsinngh/devops-learning-app:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}

