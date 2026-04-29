pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "vvee11443/myapp"
        DOCKER_TAG = "latest"
        DOCKER_CREDS = "jenkins-token"   // ← your ID
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/workdone911-coder/docker_d2.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
            }
        }

        stage('Login Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDS, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE:$DOCKER_TAG'
            }
        }
    }
}