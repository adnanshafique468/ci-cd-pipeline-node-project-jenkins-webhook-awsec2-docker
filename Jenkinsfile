pipeline {
    agent any

    environment {
        IMAGE_NAME = "modern-website-image"
        CONTAINER_NAME = "modern-website-container"
        PORT = "3000"
        EMAIL = "adnanshafiq476@gmail.com"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/adnanshafique468/ci-cd-pipeline-node-project-jenkins-webhook-awsec2-docker'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Send Email Notification') {
            steps {
                emailext(
                    subject: "Modern Website Deployed Successfully 🚀",
                    body: "Your website is live at http://EC2-IP:${PORT}",
                    to: "${EMAIL}"
                )
            }
        }
    }
}