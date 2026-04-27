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
                sh 'mvn clean package'
            }
        }
    }
}