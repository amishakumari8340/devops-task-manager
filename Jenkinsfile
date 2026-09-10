pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-task-manager:1.0 .'
            }
        }

        stage('Load Image into Kind') {
            steps {
                sh 'kind load docker-image devops-task-manager:1.0 --name devops-cluster'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'kubectl rollout status deployment/devops-task-manager'
            }
        }
    }
}
