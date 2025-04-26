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
                docker { 
                    image 'maven:3.8.4'  // Usando la versión que ya funciona
                    args '-v $HOME/.m2:/root/.m2'  // Cache para Maven
                }
            }
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("-f Dockerfile ${IMAGE_NAME} .")
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
