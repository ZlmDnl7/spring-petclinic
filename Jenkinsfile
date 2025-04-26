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
            agent {
                docker { image 'maven:3.8.5-jdk-17' } 
            }
            steps {
                sh './mvnw clean package'
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
                    docker.withRegistry('', 'dockerhub') {
                        docker.image("${IMAGE_NAME}").push()
                    }
                }
            }
        }
    }
}
