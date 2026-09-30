pipeline {
    agent any

    // Use Jenkins Global Tool Configuration if you configured NodeJS via Jenkins UI:
    // tools {
    //     nodejs 'NodeJS-20' // Uncomment if you configured NodeJS under Manage Jenkins > Tools
    // }

    environment {
        CI = 'true' // Prevents interactive prompts and ensures test runners (like Jest) exit automatically
    }

    options {
        timeout(time: 20, unit: 'MINUTES')
        disableConcurrentBuilds()
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
                echo 'Installing packages...'
                // Use 'npm ci' if you have a package-lock.json (clean, reproducible install)
                // Otherwise fallback to 'npm install'
                sh 'npm ci || npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Building frontend/backend...'
                // Runs the "build" script from your package.json (if present)
                sh 'npm run build --if-present'
            }
        }

        stage('Test') {
            steps {
                echo 'Executing test suite...'
                // Runs tests in non-watch/CI mode; --if-present prevents failure if test script is empty
                sh 'npm test --if-present -- --watchAll=false'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished. Cleaning workspace...'
            cleanWs()
        }
        success {
            echo 'Node.js build and tests passed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs above for build or test errors.'
        }
    }
}