pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'ff174281-41e5-493a-9951-8591522489be', branch: 'main', url:'https://github.com/CPazL/pin1.git'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Building..."'
                sh 'npm install'
                // Agrega otros comandos de compilación
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Testing..."'
                sh 'npm test'
                // Agrega comandos de prueba
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('mi-app:latest')
                }
            }
        }
    stage('Push to Registry') {
        steps {
            withDockerRegistry([ credentialsId: '655d9ba6-2177-4c22-b40f-97f535eeca93', url: 'http://localhost:5000' ]) {
                sh 'docker tag mi-app:latest localhost:5000/mi-app:latest'
                sh 'docker push localhost:5000/mi-app:latest'
            }
        }
    }

    }
}
