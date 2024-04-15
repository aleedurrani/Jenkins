pipeline {
    agent any

    stages {
        
        stage('Dependency Installation') {
            steps {
                
                bat 'npm install' 
            }
        }
        
        stage('Build Docker Image') {
            steps {
                
                echo 'Build Image'
            }
        }
        
        stage('Run Docker Image') {
            steps {
                
                echo 'Run Image'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                
                echo 'Push'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed :('
        }
    }
}
