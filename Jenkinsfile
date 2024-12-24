pipeline {
    agent {
        pipeline {
            image 'python:3.9-slim' // Используем образ Python
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    sh 'apt-get update && apt-get install -y git'
                }
                checkout scm
            }
        }

        stage('Run Application') {
            steps {
                script {
                    sh 'chmod +x app.py' // Убедимся, что файл исполняемый
                    sh 'python app.py'   // Запустим app.py
                }
            }
        }
    }

    post {
        success {
            echo 'Script executed successfully!'
        }
        failure {
            echo 'Script execution failed!'
        }
    }
}
