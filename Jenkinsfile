pipeline {
    agent any

    tools{
        maven 'M3'
    }

    stages {
        stage('Git Clone') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'webhook_benjamin', url: 'https://github.com/BenjaminRuiz141/sucursal_vehiculos']])
            }
        }
        stage('Build Aplication - Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Image') {
            steps {
                sh 'docker build -t vehiculosbuild_img .'
            }
        }
        stage('Deployment') {
            steps {
                sh 'docker stop vehiculosBuild || true'
                sh 'docker rm vehiculosBuild || true'
                sh 'docker run -d -p 9090:8080 --name vehiculosBuild vehiculosBuild_img'
            }
        }
    }
}
