pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "hudjo712/ci-cd-demo:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'b9e3076c-5e67-4eee-97c0-17184f698c47',
                    branch: 'main',
                    url: 'git@github.com:HudJo712/DEVOP1-HudJo712-.git'
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    docker run --rm \
                    -v $WORKSPACE:/app -w /app \
                    python:3.9 bash -c "pip install -r requirements.txt && pytest tests/"
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
