pipeline {
    agent any

    tools {
        nodejs 'Node 18'
    }

    environment {
        IMAGE_NAME = 'node-app'
        IMAGE_TAG = 'latest'
        CONTAINER_NAME = "${IMAGE_NAME}_container"
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
                sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
            }
        }

        stage('Run Docker Container') {
            steps {
                // Stop any existing container with same name
                sh "docker rm -f $CONTAINER_NAME || true"

                // Run new container
                sh "docker run -d -p 3002:80 --name $CONTAINER_NAME $IMAGE_NAME:$IMAGE_TAG"
            }
        }

        stage('Docker Status') {
            steps {
                echo '--- Docker Images ---'
                sh 'docker images'

                echo '--- Running Containers ---'
                sh 'docker ps -a'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
        // Remove this if you want to keep the container running
        // always {
        //     echo 'Cleaning up...'
        //     sh "docker rm -f $CONTAINER_NAME || true"
        // }
    }
}
