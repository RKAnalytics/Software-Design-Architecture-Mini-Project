pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t myapp:v1 .'
            }
        }

        stage('Push') {
            steps {
                sh 'docker tag myapp:v1 yourdockerhub/myapp:v1'
                sh 'docker push yourdockerhub/myapp:v1'
            }
        }

        stage('Deploy') {
            steps {
                sh 'kubectl apply -f kubernetes/deployment.yaml'
                sh 'kubectl apply -f kubernetes/service.yaml'
            }
        }
    }
}