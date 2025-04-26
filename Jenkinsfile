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
                    image 'maven:3.8.4'  // Usando la versión de la práctica
                    args '-v $HOME/.m2:/root/.m2'  // Cache de Maven
                }
            }
            steps {
                sh 'mvn clean package'  // Cambiado de ./mvnw a mvn
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
