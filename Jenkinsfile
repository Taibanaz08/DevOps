
pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                echo 'Cloning repository'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myweb:v1 .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d --rm -p 8090:80 --name myweb-container myweb:v1'
            }
        }
    }
}