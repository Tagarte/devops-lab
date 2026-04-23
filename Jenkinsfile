pipeline {
    agent any
	
    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Tagarte/devops-lab.git'
            }
        }

        stage('Build Docker') {
            steps {              
				bat 'docker build -t webapp:latest .'

            }
        }

        stage('Deploy Kubernetes') {
            steps {		
                bat 'kubectl apply -f deployment.yaml'
				bat 'kubectl apply -f service.yaml'	
            }
        }
    }
}