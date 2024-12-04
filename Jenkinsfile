pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                bat 'docker build -t flask-todo-app .'
            }
        }
        
        stage('Test') {
            steps {
                bat 'docker run flask-todo-app python -m unittest discover tests'
            }
        }
        
        stage('Push to Registry') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'lord6rimm', passwordVariable: 'Hello,5384')]) {
                    bat """
                        docker login -u lord6rimm -p Hello,5384
                        docker tag flask-todo-app lord6rimm/flask-todo-app:latest
                        docker push lord6rimm/flask-todo-app:latest
                    """
                }
            }
        }
    }
}
