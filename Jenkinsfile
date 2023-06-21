pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/master']], 
                          userRemoteConfigs: [[url: 'https://github.com/h-h123/ToDo-List.git']]])
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'python manage.py test'
            }
        }
        
        stage('Collect Static Files') {
            steps {
                sh 'python manage.py collectstatic --noinput'
            }
        }
        
        stage('Migrate Database') {
            steps {
                sh 'python manage.py migrate'
            }
        }
        
        stage('Run Server') {
            steps {
                sh 'python manage.py runserver'
            }
        }
    }
}
