pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/shekar55/DockerSwarm.git']])
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t chandu5562/python:latest .'
            }
        }
    stage('Push Docker image') {
            environment {
                DOCKER_HUB_LOGIN = credentials('docker')
            }
            steps {
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
                sh  'docker push chandu5562/python:latest'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker swarm init'
                sh 'docker stack deploy --compose-file docker-compose.yml python'
            }
        }
    }
}
