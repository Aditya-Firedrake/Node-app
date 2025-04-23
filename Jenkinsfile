pipeline {
    agent any

    tools {
        nodejs 'Node 18'
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
    }
}
