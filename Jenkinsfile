pipeline {
    agent any

    environment {
        CI = 'true'
    }

    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    stages {
        stage('Build') {
            steps {
                echo 'Running build phase...'
                // Replace with your project build command (e.g., sh 'npm run build' or sh 'mvn compile')
                sh 'echo "Building project..."'
            }
        }

        stage('Test') {
            steps {
                echo 'Running test phase...'
                // Replace with your project test command (e.g., sh 'npm test' or sh 'mvn test')
                sh 'echo "Testing project..."'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
            cleanWs()
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}