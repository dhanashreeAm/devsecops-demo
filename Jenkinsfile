pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Build') {
            steps {
                bat 'python app.py'
            }
        }

        stage('Test') {
            steps {
                bat 'python -m pytest'
            }
        }

        stage('Secret Scan') {
            steps {
                bat 'gitleaks dir . --config .gitleaks.toml --redact --exit-code 1'
            }
        }

stage('SAST - Bandit') {
            steps {
                bat 'python -m bandit -r . -ll'
            }
        }
    }

    post {
        success {
            echo 'CI + Security Pipeline completed successfully!'
        }

        failure {
            echo 'Security/CI gate failed!'
        }
    }
}