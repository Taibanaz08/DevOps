pipeline {
    agent any

    environment {
        IMAGE_NAME = "taibanaz/myweb:v2"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Taibanaz08/DevOps.git', branch: 'main'
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
                    
                    bat "docker logout"

                    // IMPORTANT: Windows friendly login (no stdin issue)
                    bat "docker login -u %USER% -p %PASS%"

                }
            }
        }

        stage('Push Image') {
            steps {
                bat "docker push %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline SUCCESS - Image pushed to DockerHub"
        }
        failure {
            echo "❌ Pipeline FAILED - Check logs"
        }
    }
}