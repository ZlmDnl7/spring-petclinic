pipeline {
    agent none
    stages {
        stage('Maven Install') {
            agent {
                docker {
                    image 'maven:3.8.4'
                }
            }
            steps {
                sh 'mvn clean install'
            }
        }
    }
}
