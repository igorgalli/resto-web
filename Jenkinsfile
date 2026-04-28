pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'JDK25'
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
        stage('Run') {
            steps {
                bat 'java -jar target\\pizzeria-web-0.0.1-SNAPSHOT.jar'
            }
        }
    }
}