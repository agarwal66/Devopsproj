pipeline {
    agent any

    environment {
        IMAGE_NAME = "code-friends-app"
        CONTAINER_NAME = "code-friends-container"
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning Repository...'
                git url: 'https://github.com/agarwal66/Devopsproj.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js Dependencies...'
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker Container...'
                sh 'docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }

        stage('Test App') {
            steps {
                echo 'Testing app...'
                sh 'sleep 10 && curl -f http://localhost:3000 || echo "App might not be running."'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up Docker container and image...'
            sh 'docker rm -f $CONTAINER_NAME || true'
            sh 'docker rmi $IMAGE_NAME || true'
        }
    }
}
