node {
    git poll: true, url: 'https://github.com/Geonhee-LEE/Docker_Jenkins.git'
    
    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'geonhee',
usernameVariable: 'DOCKER_USER_ID', passwordVariable: 'DOCKER_USER_PASSWORD']]) {
        stage('Pull') {
            git 'https://github.com/Geonhee-LEE/Docker_Jenkins.git'
        }
        stage('Unit Test') {
            sh(script: 'docker-compose run --rm unit')
        }
        stage('Build') {
            sh(script: 'docker-compose build app')
        }
        stage('Tag') {
            sh(script: 'docker tag ${DOCKER_USER_ID}/ubuntu ${DOCKER_USER_ID}/ubuntu:${BUILD_NUMBER}')
        }
        stage('Push') {
            sh(script: 'docker login -u ${DOCKER_USER_ID} -p ${DOCKER_USER_PASSWORD}')
            sh(script: 'docker push ${DOCKER_USER_ID}/ubuntu:${BUILD_NUMBER}')
            sh(script: 'docker push ${DOCKER_USER_ID}/ubuntu:latest')
        }
        stage('Deploy') {
            sh(script: 'docker-compose up -d production')
        }
    }
}
