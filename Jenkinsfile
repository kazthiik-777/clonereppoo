pipeline {
    agent any

    tools {
        nodejs 'NodeJS-20' // This must match the name you set in Tools
    }

    environment {
        CI = 'true'
    }

    stages {
        stage('Verify Environment') {
            steps {
                sh 'node -v'
                sh 'npm -v'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm ci || npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build --if-present'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test --if-present -- --watchAll=false'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}