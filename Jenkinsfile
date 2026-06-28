pipeline {
    agent any

    options {
        timeout(time: 20, unit: 'MINUTES')
    }

    environment {
        IMAGE_NAME = "taibanaz/myweb:${BUILD_NUMBER}"
        DEPLOYMENT_NAME = "myweb-deployment"
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
                bat "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {

                    bat "docker logout"

                    // Windows stable login
                    bat "docker login -u %USER% -p %PASS%"
                }
            }
        }

        stage('Push Image') {
            steps {
                bat "docker push ${IMAGE_NAME}"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat "kubectl apply -f deployment.yaml"
                bat "kubectl apply -f service.yaml"

                // wait for rollout (IMPORTANT for production)
                bat "kubectl rollout status deployment/%DEPLOYMENT_NAME%"
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
            echo "Pipeline SUCCESS 🚀 Image deployed: ${IMAGE_NAME}"
        }

        failure {
            echo "Pipeline FAILED ❌ Check logs"
        }

        always {
            // cleanup Docker space
            bat "docker system prune -f"
        }
    }
}