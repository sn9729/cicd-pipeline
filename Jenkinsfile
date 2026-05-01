pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build --no-cache -t myapp:v2 .'
            }
        }

        stage('Load Image to Minikube') {
            steps {
                bat 'minikube image load myapp:v2'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat '''
                set KUBECONFIG=C:\\Users\\mailt\\.kube\\config
                kubectl set image deployment/myapp myapp=myapp:v2 --record || exit 0
                kubectl apply -f deployment.yaml
                kubectl rollout restart deployment myapp
                kubectl rollout status deployment/myapp
                '''
            }
        }

    }

    post {
        success {
            echo 'Deployment Successful'
        }
        failure {
            echo 'Deployment Failed'
        }
    }
}