pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sanjanar27mys/myjavaapp"
        DOCKER_TAG = "v1"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/sanjana-mys/java-docker-jenkins.git'
            }
        }

        stage('Build Java') {
            steps {
                bat 'javac HelloWorld.java'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:%DOCKER_TAG% .'
            }
        }

        stage('Login Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%:%DOCKER_TAG%'
            }
        }
    }
}