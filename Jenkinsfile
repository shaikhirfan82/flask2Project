pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/shaikhirfan82/flask2Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-jenkins .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f flask_app || true
                docker run -d -p 5000:5000 --name flask_app flask-jenkins
                '''
            }
        }
    }
}
