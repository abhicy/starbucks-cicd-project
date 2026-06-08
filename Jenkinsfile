pipeline {
    agent any

    tools {
        nodejs 'node16'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/abhicy/starbucks-cicd-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t starbucks-app .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker tag starbucks-app abhi15121994/starbucks-app:latest
                    docker push abhi15121994/starbucks-app:latest
                    '''
                }
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                docker stop starbucks-app-container || true
                docker rm starbucks-app-container || true

                docker pull abhi15121994/starbucks-app:latest

                docker run -d \
                --name starbucks-app-container \
                -p 3000:3000 \
                abhi15121994/starbucks-app:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline Executed Successfully!'
        }
    }
}
