pipeline {
    agent any

    environment {
        IMAGE_NAME = "rakeshs53350/devops-capstone-app"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/RS-cloud-intellipaat/devops-capstone-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $IMAGE_NAME:latest
                    '''
                }
            }
        }
    }
}
