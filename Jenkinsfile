pipeline {
    agent any

    environment {
        IMAGE_NAME = "demo-app"
        REGISTRY = "my-docker-hub"  // Changez par votre registre Docker
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build & Push') {
            steps {
                sh 'docker build -t $REGISTRY/$IMAGE_NAME:latest .'
                sh 'docker push $REGISTRY/$IMAGE_NAME:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
