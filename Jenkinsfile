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
                bat 'start /B java -jar target\\*.jar'
            }
        }
    }
}