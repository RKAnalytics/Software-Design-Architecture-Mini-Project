pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Building Docker image manually already done"
            }
        }

        stage('Push') {
            steps {
                echo "Image already pushed to Docker Hub"
            }
        }

        stage('Deploy') {
            steps {
                sh 'kubectl rollout restart deployment flask-app'
            }
        }
    }
}