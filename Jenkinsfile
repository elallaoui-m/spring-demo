pipeline {
    agent any
    def app
    // triggers {
    //     pollSCM 'H * * * *'
    // }
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
            app = docker.build("elwiqo/spring-demo")
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'docker-creds') {            
                app.push("${env.BUILD_NUMBER}")            
                app.push("latest")        
            }    
        }
    }
}
