pipeline {
agent any

```
environment {
    IMAGE_NAME = "rakeshs53350/devops-capstone-app"
}

stages {

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

    stage('Deploy to Kubernetes') {
        steps {
            sh '''
            kubectl apply -f deployment.yaml
            kubectl apply -f service.yaml
            kubectl rollout restart deployment devops-capstone-app
            '''
        }
    }
}
```

}
