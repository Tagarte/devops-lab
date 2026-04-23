pipeline {
    agent any

    environment {
        KUBECONFIG = "C:\\ProgramData\\Jenkins\\.kube\\config"
    }

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
                bat 'kubectl apply -f deployment.yaml --validate=false'
				bat 'kubectl apply -f service.yaml --validate=false'	
				bat 'kubectl rollout restart deployment webapp'
            }
        }
    }
}