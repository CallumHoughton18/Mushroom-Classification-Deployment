pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }

    stages {
        stage('Copy files') {
            withCredentials([file(credentialsId: 'docker.env-file', variable: 'DOCKER-ENV'),
            file(credentialsId: 'nginx.conf-file', variable: 'NGINX-CONF')]) {
                sh "cp \$DOCKER-ENV ./.docker.env"
                sh "cp \$NGINX-CONF ./nginx/nginx.conf"
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