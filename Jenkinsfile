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
                
                bat 'docker build -t my_image .'
            }
        }
        
        stage('Run Docker Image') {
            steps {
                
                bat 'docker run -d -p 3000:3001 my_image'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                
                bat 'docker push my_image'
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
