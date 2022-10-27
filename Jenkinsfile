pipeline {
    agent any

    stages {
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipeline -t inewthinker/todo-be:latest --target builder .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipeline -t inewthinker/todo-be:latest --target delivery .'
            }
        }
          stage('Cleanup stage') {
            steps {
                sh 'yes | docker system prune '
            }
        }
    }
}
