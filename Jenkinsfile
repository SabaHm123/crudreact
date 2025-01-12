pipeline {
    agent any

    environment {
        FRONTEND_IMAGE = 'myorg/frontend:latest'
        DOCKER_REGISTRY = 'docker.io' // Changez si nécessaire
        DOCKER_CREDENTIALS = 'docker-credentials-id' // ID des identifiants Jenkins pour Docker
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Récupération du code depuis un dépôt Git
                git branch: 'main', url: 'https://github.com/crudreact.git'
            }
        }

        

        stage('Build Frontend Docker Image') {
            steps {
                script {
                    // Construire l'image Docker du frontend
                    dir('frontend') {
                        sh 'docker build -t ${FRONTEND_IMAGE} .'
                    }
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                script {
                    withDockerRegistry([credentialsId: DOCKER_CREDENTIALS, url: "https://${DOCKER_REGISTRY}"]) {
                        sh "docker push ${FRONTEND_IMAGE}"
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé.'
        }
        success {
            echo 'Pipeline exécuté avec succès.'
        }
        failure {
            echo 'Une erreur s\'est produite.'
        }
    }
}
