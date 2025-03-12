pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Coutre/LAB-3-_DEVOPS'
            }
        }
        stage('Build') {
            steps {
                dir('myApp') {
                    sh 'mvn clean package'
                }
            }
        }
    }
}