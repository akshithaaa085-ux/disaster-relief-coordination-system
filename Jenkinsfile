pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t disaster-relief:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker rm -f disaster-app
                docker run -d -p 5000:5000 --name disaster-app disaster-relief:latest
                '''
            }
        }
    }
}