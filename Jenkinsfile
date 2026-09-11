pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code has been checked out from GitHub'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
