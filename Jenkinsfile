pipeline {

    agent any

    environment {
        IMAGE_NAME = "zomato-clone"
        CONTAINER_NAME = "zomato-container"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/maliVishal01/devops-zomato-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Security Scan (Trivy)') {
            steps {
                sh '''
                trivy image --exit-code 0 --severity HIGH,CRITICAL $IMAGE_NAME
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true
                docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
