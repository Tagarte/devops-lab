pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\ProgramData\\Jenkins\\.kube\\config'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Tagarte/devops-lab.git'
            }
        }

        stage('Build Docker') {
            steps {
                // On tag l'image avec le numéro du build Jenkins
                bat "docker build -t webapp:${env.BUILD_NUMBER} ."
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                // On met à jour le fichier deployment.yaml avec le bon tag
                bat "kubectl set image webapp webapp=webapp:${env.BUILD_NUMBER} --record"

                // On force le redéploiement pour que les pods utilisent la nouvelle image
                bat "kubectl rollout restart deployment webapp"

                // Vérification du statut du déploiement
                bat "kubectl rollout status deployment webapp"
            }
        }
    }
}
