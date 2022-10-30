pipeline {
    agent any
    stages {
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t image-builder --target builder .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t inewthinker/todo-be:jenkins-$BUILD_NUMBER --target delivery .'
            }
        }
        stage('Cleanup') {
            steps {
                echo "CLEANING!"
                sh 'docker system prune -f'
            }
        }
        stage('push') {
            environment {
                dockerpwd = credentials('docker_pwd')
            }
            steps {
                    sh 'docker login -u inewthinker -p ${dockerpwd}'
                    sh "docker push inewthinker/todo-be:jenkins-$BUILD_NUMBER"
        }
    }
}
}
