pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }
    
    triggers {
        [$class: 'DockerHubTrigger', options: [[$class: 'TriggerOnSpecifiedImageNames', repoNames: ["callumhoughton22/mushroom-api"].toSet()]]]
    }

    stages {
        stage('Copy files') {
            steps {
                withCredentials([file(credentialsId: 'docker.env-file', variable: 'DOCKER_ENV'),
                file(credentialsId: 'nginx.conf-file', variable: 'NGINX_CONF')]) {
                    sh "cp \$DOCKER_ENV ./.docker.env"
                    sh "cp \$NGINX_CONF ./nginx/nginx.conf"
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