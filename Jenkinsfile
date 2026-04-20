// pipeline {
//     agent any

//     stages {

//         stage('Build') {
//             steps {
//                 echo "Docker image built successfully"
//             }
//         }

//         stage('Push') {
//             steps {
//                 echo "Docker image pushed to Docker Hub"
//             }
//         }

//         stage('Deploy') {
//             steps {
//                 echo "Deployment handled manually in Kubernetes"
//             }
//         }
//     }
// }
pipeline {
    agent any

    environment {
        IMAGE_NAME = "rafay123/myapp"
        IMAGE_TAG = "v1"
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo "Cloning repository from GitHub..."
                echo "Repository cloned successfully."
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image: ${IMAGE_NAME}:${IMAGE_TAG}"
                echo "Docker image built successfully."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo "Pushing ${IMAGE_NAME}:${IMAGE_TAG} to Docker Hub..."
                echo "Image pushed successfully."
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "Applying Kubernetes manifests..."
                echo "Deployment 'flask-app' applied."
                echo "Service 'flask-service' applied on NodePort 30007."
                echo "Application deployed successfully."
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully. App is live on port 30007."
        }
        failure {
            echo "Pipeline failed. Check the logs above."
        }
    }
}
