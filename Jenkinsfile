pipeline {
    agent any
    stages {
        stage("Build") {
            steps { sh "npm install" }
        }
        stage("Test") {
            steps { sh "npm test" }
        }
        stage("Docker Build & Push") {
            steps {
                sh "docker build -t devops-learning-app ."
                sh "docker push devops-learning-app"
            }
        }
        stage("Deploy to Kubernetes") {
            steps { sh "kubectl apply -f deployment.yaml" }
        }
    }
}
