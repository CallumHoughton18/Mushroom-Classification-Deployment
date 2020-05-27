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
                    sh "cp \$DOCKER_ENV ./.docker.env"
                    sh "cp \$NGINX_CONF ./nginx/nginx.conf"
                }
            }
        }
        stage('Deploy via Docker-Compose') {
            steps {
                sh 'docker-compose -f docker-compose.prod.yml up -d --build'
                sh 'docker system prune -a -f'
            }
        }
    }
    
    post {
        always {
            withCredentials([string(credentialsId: 'sendto-email', variable: 'EMAIL')]) {
                emailext( to: "${EMAIL}", 
                    body: "${env.BUILD_URL}", 
                    subject: "[${currentBuild.currentResult}] ${env.JOB_NAME} - Build # ${env.BUILD_NUMBER}",
                    attachLog: true)
            }
            deleteDir()      
        }
        cleanup {
            deleteDir()
        }
    }
}