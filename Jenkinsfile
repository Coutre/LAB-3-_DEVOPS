pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials'
        DOCKER_IMAGE = 'coutre/myapp:v1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Coutre/LAB-3-_DEVOPS'
            }
        }

        stage('Build Maven Project') {
            steps {
                dir('myApp'){
                    bat 'mvn clean package' 
                }            
            }
        }

        stage('Check Docker') {
            steps {
                bat 'docker --version'
                bat 'docker ps'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat "echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('myApp'){
                    bat "docker build -t %DOCKER_IMAGE% ."
                }

            }
        }

        stage('Push Docker Image') {
            steps {
                dir('myApp'){
                    bat "docker push %DOCKER_IMAGE%"   
                }
            }
        }
    }
}
