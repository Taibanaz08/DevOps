pipeline {
    agent any

    environment {
        IMAGE_NAME = "taibanaz/myweb:v2"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Taibanaz08/DevOps.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t taibanaz/myweb:v2 ."
            }
        }

        

        stage('Push Image') {
            steps {
                bat "docker push taibanaz/myweb:v2"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat "kubectl apply -f deployment.yaml"
                bat "kubectl apply -f service.yaml"
            }
        }

        stage('Verify Deployment') {
            steps {
                bat "kubectl get pods"
                bat "kubectl get svc"
            }
        }
    }

    post {
        success {
            echo "Pipeline SUCCESS 🚀 Application deployed successfully"
        }
        failure {
            echo "Pipeline FAILED ❌ Check logs"
        }
    }
}