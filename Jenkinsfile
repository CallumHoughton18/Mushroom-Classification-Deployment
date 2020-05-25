pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }

    stages {
        stage('Copy files') {
            steps {
                withCredentials([file(credentialsId: 'mushroomapi_docker.env', variable: 'DOCKER_ENV'),
                file(credentialsId: 'mushroomapi_nginx.conf', variable: 'NGINX_CONF')]) {
                    sh "cp -- \$DOCKER_ENV ./"
                    sh "cp -- \$NGINX_CONF ./"
                }
            }
        }
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