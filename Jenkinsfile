pipeline {

    environment {
    registry = "elwiqo/spring-demo"
    registryCredential = 'elwiqo'
    dockerImage = ''
    }
    agent any

    triggers {
        pollSCM 'H * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew assemble'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
    }
}
