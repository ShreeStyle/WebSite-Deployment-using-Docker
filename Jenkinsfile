stage('Build Docker Image') {
    steps {
        sh '''
        /opt/homebrew/bin/docker --version
        /opt/homebrew/bin/docker build -t website-image .
        '''
    }
}