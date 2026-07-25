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
                sh '''
                export PATH=/opt/homebrew/bin:/Applications/Docker.app/Contents/Resources/bin:$PATH

                docker --version
                docker build -t website-image .
                '''
            }
        }
    }
}