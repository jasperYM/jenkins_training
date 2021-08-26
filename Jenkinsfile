pipeline {
    environment {
        registry = 'israelaminu/ml_model'
        registryCredential = 'dockerhub_id'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Build Docker Image') {
            agent any
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
		stage('test flask app') {
            agent any
            steps {
                sh 'curl host.docker.internal:8080/prometheus'
                }
            }
        stage('Remove Unused docker image') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}