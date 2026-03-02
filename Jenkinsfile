pipeline {
    agent any

    tools{
        maven 'M3'
    }

    stages {
        stage('Git Clone') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Webhook_benjamin', url: 'https://github.com/BenjaminRuiz141/sucursal_vehiculos']])
            }
        }
        stage('Build Aplication - Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Image') {
            steps {
                sh 'docker build -t imagen_vehiculos .'
            }
        }
        stage('Deployment') {
            steps {
                sh 'docker stop contenedor_sucursal || true'
                sh 'docker rm contenedor_sucursal || true'
                sh 'docker run -d -p 9090:8080 --name contenedor_sucursal imagen_vehiculos'
            }
        }
    }
}
