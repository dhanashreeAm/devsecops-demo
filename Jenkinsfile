pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out'
            }
        }

        stage('Check Python') {
            steps {
                bat 'python --version'
                bat 'where python'
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

    }

    post {

        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed!'
        }

    }
}
