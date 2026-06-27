pipeline {
    agent any

    environment {
        IMAGE_NAME = "taibanaz/myweb:v2"
        KUBECONFIG = "C:\\Users\\vsoft\\.kube\\config"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Taibanaz08/DevOps.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Load Image to Kind') {
            steps {
        bat "kind load docker-image taibanaz/myweb:v2 --name devops-cluster"
    }
}

        stage('Deploy to Kubernetes') {
            steps {
                bat """
                set KUBECONFIG=%KUBECONFIG%
                kubectl set image deployment/myweb-deployment myweb=%IMAGE_NAME%
                kubectl rollout status deployment/myweb-deployment
                """
            }
        }
    }
}