pipeline {
    agent any

    stages {
        stage('Build Backend') {
            steps {
                sh 'docker build -t dockerizzz/todo-backend ./backend'
            }
        }
        stage('Build Frontend') {
            steps {
                sh 'docker build -t dockerizzz/todo-frontend ./frontend'
            }
        }
        stage('Push Images') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub-token', variable: 'DOCKER_HUB_TOKEN')]) {
                    sh 'echo $DOCKER_HUB_TOKEN | docker login -u dockerizzz --password-stdin'
                    sh 'docker push dockerizzz/todo-backend'
                    sh 'docker push dockerizzz/todo-frontend'
                }
            }
        }
        stage('Deploy to K8s') {
            steps {
                sh 'kubectl apply -f k8s-manifests/'
            }
        }
    }
}
