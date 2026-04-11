pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Docker image built successfully"
            }
        }

        stage('Push') {
            steps {
                echo "Docker image pushed to Docker Hub"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment handled manually in Kubernetes"
            }
        }
    }
}