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
                sh './mvnw package'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Docker Push') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerhub', url: '' ]) {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }
    }
}
