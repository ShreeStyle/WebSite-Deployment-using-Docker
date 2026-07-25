pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t website-image .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh '''
                docker rm -f website-container || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                --name website-container \
                -p 8081:80 \
                website-image
                '''
            }
        }

        stage('Test Website') {
            steps {
                sh '''
                sleep 5
                curl http://localhost:8081
                '''
            }
        }

    }
}