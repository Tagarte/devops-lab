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
				sh 'docker build -t webapp:latest .'

            }
        }

        stage('Deploy Kubernetes') {
            steps {		
                sh 'kubectl apply -f deployment.yaml'
				sh 'kubectl apply -f service.yaml'	
            }
        }
    }
}