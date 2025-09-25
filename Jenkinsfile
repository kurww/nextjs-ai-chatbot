pipeline {
    agent any
    tools {
        nodejs "my-nodejs"
    }
    stages {
        stage("Build") {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage("Start") {
            steps {
                sh 'npm start'
                echo "App started successfully"
            }
        }
    }
}
