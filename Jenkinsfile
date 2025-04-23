pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    tools {
        nodejs 'NodeJS 18' // Make sure this matches the name of your Node.js tool in Jenkins config
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'npm run build' // optional, if you have a build step
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying application...'
                // Example: sh './scripts/deploy.sh'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            cleanWs()
        }

        failure {
            echo 'Pipeline failed!'
        }

        success {
            echo 'Pipeline completed successfully!'
        }
    }
}
