pipeline {
    agent any

    environment {
        IMAGE = "taibanaz/myweb:v2"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Taibanaz08/DevOps.git'
            }
        }

        stage('Build Image') {
            steps {
                bat "docker build -t %IMAGE% ."
            }
        }

        stage('Push Image to DockerHub') {
            steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
            bat "echo %PASS% | docker login -u %USER% --password-stdin"
            bat "docker push taibanaz/myweb:v2"
        }
    }
}

        stage('Deploy to K8s') {
            steps {
                bat "kubectl set image deployment/myweb-deployment myweb=%IMAGE%"
                bat "kubectl rollout status deployment/myweb-deployment"
            }
        }

        stage('Verify') {
            steps {
                bat "kubectl get pods"
                bat "kubectl get svc"
            }
        }
    }
}