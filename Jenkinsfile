pipeline {
    agent any
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
           steps {
                dockerBuildAndPublish {
                    repositoryName('elwiqo/spring-demo')
                    tag('${BUILD_TIMESTAMP}-${GIT_REVISION,length=7}')
                    registryCredentials('docker-creds')
                    forcePull(false)
                    createFingerprints(false)
                    skipDecorate()
                }
            }
        }

        
    }
}
