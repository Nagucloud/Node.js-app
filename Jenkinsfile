pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nagucloud/Node.js-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t nagucloud/nodejsapplication:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh "echo Bloom@6248 | docker login -u nagucloud --password-stdin"
                sh "docker push nagucloud/nodejsapplication:latest"
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f nodejs-demo || true
                    docker run -d -p 3000:3000 --name nodejs-demo nagucloud/nodejsapplication:latest
                '''
            }
        }
    }
}
