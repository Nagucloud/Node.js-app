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
                sh "docker build -t $Nagu/nodejs-jenkins-demo:latest ."
            }
        }
        stage('Push to Docker Hub') {
            steps {
                sh "echo docker login -u nagucloud -p Bloom@6248
                sh "docker push $Nagu/nodejs-jenkins-demo:latest"
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f nodejs-demo || true
                    docker run -d -p 3000:3000 --name nodejs-demo $nagu/nodejs-jenkins-demo:latest
                '''
            }
        }
    }
}
