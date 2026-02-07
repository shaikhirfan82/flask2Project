pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-jenkins"
        CONTAINER_NAME = "flask_app"
    }

    stages {

        stage('Check Docker') {
            steps {
                sh '''
                echo "Running as user:"
                whoami
                echo "Docker version:"
                docker --version
                '''
            }
        }

        stage('Clone Repo') {
            steps {
                git 'https://github.com/shaikhirfan82/flask2Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true
                docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Flask app deployed successfully"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
