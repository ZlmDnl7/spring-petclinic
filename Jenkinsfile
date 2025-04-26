pipeline {
    agent any
    environment {
        IMAGE_NAME = "daniarias7/spring-petclinic"
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
        stage('Docker Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials-id') {
                        docker.image("${IMAGE_NAME}").push('latest')
                    }
                }
            }
        }
    }
}
