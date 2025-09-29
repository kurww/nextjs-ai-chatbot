pipeline {
    agent {
        docker {
            image 'node:20'  
            args '-u root:root'
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_REPO = "adkurnwn/nextjs-ai-chatbot"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kurww/nextjs-ai-chatbot.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Next.js') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    sh "docker build -t $DOCKERHUB_REPO:${env.BUILD_NUMBER} ."
                }
            }
        }

        stage('Docker Login & Push') {
            steps {
                script {
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh "docker push $DOCKERHUB_REPO:${env.BUILD_NUMBER}"
                }
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
