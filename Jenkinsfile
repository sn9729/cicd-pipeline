pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp:v1 .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat '''
                set KUBECONFIG=C:\\Users\\mailt\\.kube\\config
                kubectl config current-context
                kubectl apply -f deployment.yaml
                '''
            }
        }

    }
}