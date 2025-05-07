pipeline {
 agent any
 environment {
 DOCKER_IMAGE = "hudjo712/ci-cd-demo:latest"
 }
 stages {
 stage('Checkout') {
 steps {
 git 'https://github.com/HudJo712/DEVOP1-HudJo712-'
 }
 }
 stage('Run Tests') {
 steps {
 sh 'pytest tests/'
 }
 }
 stage('Build Docker Image') {
 steps {
 sh 'docker build -t $DOCKER_IMAGE .'
 }
 }
 stage('Push Docker Image') {
 steps {
 withDockerRegistry([credentialsId: 'docker-hub-creds', url:
'']) {
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