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

        stage('Remove Old Container') {
            steps {
                sh '''
                export PATH=/opt/homebrew/bin:/Applications/Docker.app/Contents/Resources/bin:$PATH

                docker rm -f website-container || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                export PATH=/opt/homebrew/bin:/Applications/Docker.app/Contents/Resources/bin:$PATH

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

                STATUS=$(curl -o /dev/null -s -w "%{http_code}" http://localhost:8081)

                if [ "$STATUS" = "200" ]; then
                    echo "Website deployed successfully"
                else
                    echo "Website deployment failed"
                    exit 1
                fi
                '''
            }
        }
    }
}