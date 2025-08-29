pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-cred')  // Jenkins credential ID cho DockerHub
        DOCKERHUB_USER = "thuampham777"  // Thay bằng DockerHub username
        IMAGE_NAME = "cloudhcmus_lab01_fe"          // Tên image
        GIT_REPO = "https://github.com/ThuanPham777/CloudHCMUS_Lab01_FE.git"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                echo "No build step for static HTML/JS project"
                sh 'ls -la'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    sh """
                        echo "Building Docker image..."
                        docker build -t ${DOCKERHUB_USER}/${IMAGE_NAME}:latest .
                    """
                }
            }
        }

        stage('Docker Login & Push') {
            steps {
                script {
                    sh """
                        echo "Logging in to DockerHub..."
                        echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin

                        echo "Pushing image to DockerHub..."
                        docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:latest
                    """
                }
            }
        }
    }
}
