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
                script {
                    dir('myApp') { 
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    withDockerRegistry([credentialsId: DOCKER_HUB_CREDENTIALS]) {
                        echo "Logged into Docker Hub successfully."
                    }
                }
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                script {
                    dir('myApp') {
                        def image = docker.build(DOCKER_IMAGE)
                        image.push()
                    }
                }
            }
        }
    }
}
