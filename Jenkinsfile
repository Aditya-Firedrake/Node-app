pipeline {
    agent any

    tools {
        nodejs 'Node 18'
    }

    environment {
        IMAGE_NAME = 'node-app'       // Customize this if needed
        IMAGE_TAG = 'latest'
        DOCKER_REGISTRY = ''          // Optional: Add your DockerHub or other registry here
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Aditya-Firedrake/Node-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run -d -p 3000:3000 --name ${IMAGE_NAME}_container $IMAGE_NAME:$IMAGE_TAG"
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Optional: Stop and remove container if needed
            sh "docker rm -f ${IMAGE_NAME}_container || true"
        }
    }
}
