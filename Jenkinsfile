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
                bat 'python -m pip install pip-audit'
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

        stage('SCA - Dependency Scan') {
            steps {
                bat 'pip-audit -r requirements.txt'
            }
        }

        stage('Docker Check') {
    steps {
        bat 'docker version'
    }
}
    }

    post {

        success {
            echo 'CI + DevSecOps security pipeline completed successfully!'
        }

        failure {
            echo 'CI/Security gate failed!'
        }
    }
}
