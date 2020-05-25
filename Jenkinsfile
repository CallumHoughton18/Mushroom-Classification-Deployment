pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }

    stages {
        stage('Deploy via Docker-Compose') {
            steps {
                sh 'docker-compose down --remove-orphans'
                sh 'docker-compose -f docker-compose.prod.yml up -d --build'
            }
        }
    }
    
    post {
        cleanup {
            deleteDir()
        }
    }
}