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

        stage('Gitleaks Version') {
    steps {
        bat 'gitleaks version'
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
        bat '''
            echo ===== GITLEAKS VERSION =====
            gitleaks version

            echo ===== CURRENT DIRECTORY =====
            cd

            echo ===== FILES =====
            dir

            echo ===== GITLEAKS SCAN =====
            gitleaks detect --source=. --redact --verbose --exit-code=1
        '''
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
