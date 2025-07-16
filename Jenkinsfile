pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo '📥 Cloning repository...'
                git 'https://github.com/panthangiEshwary/python-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🐳 Building Docker Image...'
                sh 'docker build -t python-jenkins-app .'
            }
        }

        stage('Run Container') {
            steps {
                echo '🚀 Running Docker container...'
                sh 'docker run -d -p 5000:5000 --name flask-app python-jenkins-app'
            }
        }
    }
}

