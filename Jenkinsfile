pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'JDK25'
    }

    environment {
        IMAGE_NAME = 'igorcardosogalli/pizzeria-web'
        IMAGE_TAG = 'latest'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker push %IMAGE_NAME%:%IMAGE_TAG%'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker ps -q --filter "name=pizzeria-web" && docker stop pizzeria-web
                docker ps -aq --filter "name=pizzeria-web" && docker rm pizzeria-web
                docker run -d -p 8081:8081 --name pizzeria-web igorcardosogalli/pizzeria-web:latest
                '''
            }
        }
    }
}