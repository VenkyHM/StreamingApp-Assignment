pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ACCOUNT_ID = 'YOUR_ACCOUNT_ID'

        ADMIN_REPO = 'admin-service'
        AUTH_REPO = 'auth-service'
        CHAT_REPO = 'chat-service'
        STREAM_REPO = 'stream-service'
        FRONTEND_REPO = 'streaming-frontend'
    }

    stages {

        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        /* ================= BACKEND SERVICES ================= */

        stage('Build Admin Service') {
            steps {
                dir('backend/admin-service') {
                    sh 'docker build -t admin-service .'
                }
            }
        }

        stage('Build Auth Service') {
            steps {
                dir('backend/auth-service') {
                    sh 'docker build -t auth-service .'
                }
            }
        }

        stage('Build Chat Service') {
            steps {
                dir('backend/chat-service') {
                    sh 'docker build -t chat-service .'
                }
            }
        }

        stage('Build Stream Service') {
            steps {
                dir('backend/stream-service') {
                    sh 'docker build -t stream-service .'
                }
            }
        }

        /* ================= FRONTEND ================= */

        stage('Build Frontend') {
            steps {
                dir('frontend/streaming-frontend') {
                    sh 'docker build -t streaming-frontend .'
                }
            }
        }

        /* ================= ECR LOGIN ================= */

        stage('ECR Login') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | \
                docker login --username AWS --password-stdin \
                $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
                '''
            }
        }

        /* ================= TAG & PUSH BACKEND ================= */

        stage('Push Admin Service') {
            steps {
                sh '''
                docker tag admin-service:latest $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$ADMIN_REPO:latest
                docker push $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$ADMIN_REPO:latest
                '''
            }
        }

        stage('Push Auth Service') {
            steps {
                sh '''
                docker tag auth-service:latest $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$AUTH_REPO:latest
                docker push $ACCOUNT_ID.dkr.ecr.ap-south-1.amazonaws.com/$AUTH_REPO:latest
                '''
            }
        }

        stage('Push Chat Service') {
            steps {
                sh '''
                docker tag chat-service:latest $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$CHAT_REPO:latest
                docker push $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$CHAT_REPO:latest
                '''
            }
        }

        stage('Push Stream Service') {
            steps {
                sh '''
                docker tag stream-service:latest $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$STREAM_REPO:latest
                docker push $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$STREAM_REPO:latest
                '''
            }
        }

        /* ================= FRONTEND PUSH ================= */

        stage('Push Frontend') {
            steps {
                sh '''
                docker tag streaming-frontend:latest $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$FRONTEND_REPO:latest
                docker push $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$FRONTEND_REPO:latest
                '''
            }
        }
    }
}
