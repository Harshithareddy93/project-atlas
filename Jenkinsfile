pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK17'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t project-atlas:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f project-atlas-app || true
                docker run -d -p 8081:8080 --name project-atlas-app project-atlas:latest
                '''
            }
        }
    }
}
