pipeline {
    agent any

    tools {
        nodejs 'Node 18'
    }

    environment {
        // Define environment variables if needed
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/your-username/your-nodejs-repo.git'
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
                    docker.build('my-nodejs-app')
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerhub-creds', url: '' ]) {
                    script {
                        docker.image('my-nodejs-app').push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
                // Add SSH or Kubernetes deploy logic here
            }
        }
    }
}
