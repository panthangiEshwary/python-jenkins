pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo " Cloning repository..."
                git branch: 'main', url: 'https://github.com/panthangiEshwary/python-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo ' Building Docker Image...'
                sh 'docker build -t python-jenkins-app .'
            }
        }

        stage('Run Container') {
            steps {
                echo ' Running Docker container...'
                // Stop and remove previous container if exists
                sh 'docker stop flask-app || true'
                sh 'docker rm flask-app || true'

                // Run new container
                sh 'docker run -d -p 5000:5000 --name flask-app python-jenkins-app'
            }
        }
    }
}

