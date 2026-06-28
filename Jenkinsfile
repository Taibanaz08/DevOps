pipeline {
    agent any

    environment {
        IMAGE_NAME = "taibanaz/myweb:v2"
    }

    stages {

        stage('Checkout Code') {
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

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat "echo %PASS% | docker login -u %USER% --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                bat "docker push %IMAGE_NAME%"
            }
        }

        stage('Load Image to Kind') {
            steps {
                bat "kind load docker-image %IMAGE_NAME% --name devops-cluster"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat "kubectl apply -f deployment.yaml"
                bat "kubectl apply -f service.yaml"
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