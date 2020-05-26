pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }

    stages {
        stage('Copy files') {
            steps {
                withCredentials([file(credentialsId: 'docker.env_file', variable: 'DOCKER_ENV'),
                file(credentialsId: 'nginx.conf_file', variable: 'NGINX_CONF')]) {
                    docker_env_path = $DOCKER_ENV
                    nginx_conf_path = $NGINX_CONF
                    sh "cp '${docker_env_path}' ./.docker.env"
                    sh "cp '${nginx_conf_path}' ./nginx.conf"
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