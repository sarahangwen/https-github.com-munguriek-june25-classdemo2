pipeline {
    agent any
    
    environment {
        VENV = 'venv'
        DJANGO_SETTINGS_MODULE = 'config.settings'  // Update with your project name
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/munguriek/june25-classdemo2.git'
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
                    python manage.py migrate --settings=config.settings
                '''
            }
        }
        
        
        stage('Run Tests') {
            steps {
                sh '''
                    . $VENV/bin/activate
                    python manage.py test --settings=config.settings
                '''
            }
        }
    }
    
    post {
        always {
            // Clean up virtual environment
            sh 'rm -rf $VENV || true'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}