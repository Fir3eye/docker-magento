pipeline {
    agent any
    
    environment {
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = 'magento2'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Fir3eye/docker-magento.git'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    sh "docker-compose -f docker-compose.yml up -d"
                }
            }
        }
        stage('Docker Tag and Push the Image ') {
            steps {
                script {
                    sh "docker tag alexcheng/magento2:latest dockt35t/magento2:latest"
                    sh "docker tag mysql:5.7 dockt35t/mysql:5.7"
                }
            }
        }
        stage("Push Docker Image"){
            steps{
                script {
                    docker.withRegistry('',DOCKER_PASS){
                        sh "docker push dockt35t/magento2:latest"
                        sh "docker push dockt35t/mysql:5.7"
                    }
                }
            }
        }
        stage('Down') {
            steps {
                script {
                    sh "docker-compose -f docker-compose.yml down"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh "docker run -d -p 8081:80 dockt35t/magento2:latest"
                    sh "docker run -d -p 3306:3306 dockt35t/mysql:5.7"
                }
            }
        }
    }
}
