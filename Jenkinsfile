pipeline {
    agent any
    environment {
        DOCKER_USER = 'harshsinngh'
        DOCKER_PASS = credentials('docker-hub-credentials')
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
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
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

