pipeline {
    agent any
    environment {
        VENV = 'venv'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/munguriek/june-2025-class-demo-1-django.git'
            }
        }
        stage('Set up Virtual Environment') {
            steps {
                sh '''
                python3 -m venv $VENV
                . $VENV/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }
        stage('Run Migrations') {
            steps {
                sh '''
                . $VENV/bin/activate
                python manage.py migrate
                '''
            }
        }
        stage('Run Tests') {
            steps {
                sh '''
                . $VENV/bin/activate
                python manage.py test
                '''
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
