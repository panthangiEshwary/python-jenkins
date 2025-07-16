pipeline {
    agent any

    environment {
        IMAGE_NAME = 'panthangieshwary/python-jenkins-app'
    }

    stages {
        stage('Clone') {
            steps {
                echo '📥 Cloning repository...'
                git 'https://github.com/panthangiEshwary/python-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🔧 Building Docker image...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo '📤 Pushing Docker image to Docker Hub...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying Container...'
                sh '''
                    docker stop flask-app || true
                    docker rm flask-app || true
                    docker run -d -p 5000:5000 --name flask-app $IMAGE_NAME
                '''
            }
        }
    }
}

