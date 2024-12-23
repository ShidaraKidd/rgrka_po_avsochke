pipeline {
    agent any

    environment {
        IMAGE_NAME = 'myapp' // Название Docker-образа
        REPO_URL = 'https://github.com/ShidaraKidd/rgrka_po_avsochke.git' // URL репозитория
    }

    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh 'docker stop myapp || true'
                    sh 'docker rm myapp || true'
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh '''
                    docker run -d --name myapp -p 8080:8080 ${IMAGE_NAME}:latest
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
