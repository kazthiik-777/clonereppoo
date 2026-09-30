pipeline {
agent any

```
tools {
    nodejs 'nodejs-20'
}

environment {
    CI = 'true'
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

    stage('Install Backend Dependencies') {
        steps {
            echo 'Installing backend dependencies...'
            dir('backend') {
                sh 'npm ci'
            }
        }
    }

    stage('Install Frontend Dependencies') {
        steps {
            echo 'Installing frontend dependencies...'
            dir('frontend') {
                sh 'npm ci'
            }
        }
    }

    stage('Build Frontend') {
        steps {
            echo 'Building frontend...'
            dir('frontend') {
                sh 'npm run build'
            }
        }
    }

    stage('Test Backend') {
        steps {
            echo 'Running backend tests...'
            dir('backend') {
                sh 'npm test'
            }
        }
    }

    stage('Test Frontend') {
        steps {
            echo 'Running frontend lint...'
            dir('frontend') {
                sh 'npm run lint'
            }
        }
    }
}

post {
    always {
        echo 'Pipeline finished. Cleaning workspace...'
        cleanWs()
    }

    success {
        echo 'Build and tests succeeded!'
    }

    failure {
        echo 'Pipeline failed. Check the logs above.'
    }
}
```

}

