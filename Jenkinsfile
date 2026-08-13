pipeline {
    agent any

    stages {

        stage('Setup Python') {
            steps {
                sh 'python3 -m venv venv'
                sh 'venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'venv/bin/pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-cicd-practice:v1 .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh 'docker stop jenkins-cicd-app || true'
                sh 'docker rm jenkins-cicd-app || true'
                sh 'docker run -d -p 5000:5000 --name jenkins-cicd-app jenkins-cicd-practice:v1'
            }
        }
    }
}