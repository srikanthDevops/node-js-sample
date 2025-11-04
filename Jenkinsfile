pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
    }
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/srikanthDevops/node-js-sample.git'
            }
        }        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_CREDENTIALS_USR}/nodejs-app:latest")
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-creds') {
                        docker.image("${DOCKERHUB_CREDENTIALS_USR}/nodejs-app:latest").push()
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }  
    }
}
