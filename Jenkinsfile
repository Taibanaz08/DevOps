pipeline {
    agent any

    environment {
        IMAGE_NAME = "taibanaz/myweb:v2"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Taibanaz08/DevOps.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t taibanaz/myweb:v2 .'
            }
        }

        stage('Push Docker Image') {
             steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
        )]) {
            bat 'echo Username=%DOCKER_USER%'
            bat 'echo PasswordLength && echo %DOCKER_PASS%'
        }
    }
}

        stage('Load Image to Kind') {
            steps {
                bat '"C:\\Users\\vsoft\\AppData\\Local\\Microsoft\\WinGet\\Packages\\Kubernetes.kind_Microsoft.Winget.Source_8wekyb3d8bbwe\\kind.exe"  load docker-image taibanaz/myweb:v2 --name devops-cluster'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl set image deployment/myweb-deployment myweb=taibanaz/myweb:v2'
            }
        }

        stage('Check User') {
            steps {
                bat 'whoami'
            }
        }

        stage('Check Docker') {
            steps {
                bat 'docker info'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl rollout status deployment/myweb-deployment'
            }
        }
    }
}
