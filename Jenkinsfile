
pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                sh '''
                    docker run --rm \
                      -v "$WORKSPACE:/app" \
                      -w /app \
                      python:3.12-slim \
                      sh -c "pip install --no-cache-dir -r requirements.txt && python -m unittest -v"
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and tests completed successfully'
        }

        failure {
            echo 'Build failed. Check the Jenkins console output.'
        }
    }
}
