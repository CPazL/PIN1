pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "cpazl/webapp:${env.BUILD_NUMBER}"
    DOCKER_REGISTRY = "127.0.0.1:5000"
  }

  stages {
    stage('Building image') {
      steps {
        // Construye la imagen con el nombre de tu aplicación y el número de build
        sh '''
          docker build -t ${ARTIFACT_ID} .
        '''  
      }
    }
  
    stage('Run tests') {
      steps {
        // Corre los tests dentro del contenedor de la imagen recién construida
        sh "docker run ${ARTIFACT_ID} npm test"
      }
    }

    stage('Deploy Image') {
      steps {
        // Etiqueta la imagen con la dirección del registro y la envía al registro local
        sh '''
          docker tag ${ARTIFACT_ID} ${DOCKER_REGISTRY}/${ARTIFACT_ID}
          docker push ${DOCKER_REGISTRY}/${ARTIFACT_ID}
        '''
      }
    }
  }
}
