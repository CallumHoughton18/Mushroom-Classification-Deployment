pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }

    stages {
        stage('Deploy via Docker-Compose') {
            steps {
                sh 'docker-compose --version'
            }
        }
    }
    
    post {
        cleanup {
            deleteDir()
        }
    }
}