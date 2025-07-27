pipeline {
  agent any

  environment {
    COMPOSE_CMD = "docker-compose -f docker-compose.yml"
  }

  stages {
    stage('Cloner le dépôt') {
      steps {
        git url: 'https://github.com/Strawhat0-3/devops'
      }
    }

    stage('Build des images Docker') {
      steps {
        sh "${COMPOSE_CMD} build"
      }
    }

    stage('Lancer l’application') {
      steps {
        sh "${COMPOSE_CMD} up -d"
      }
    }

    stage('Vérification des services') {
      steps {
        sh "${COMPOSE_CMD} ps"
      }
    }
  }

  post {
    always {
      echo "Pipeline terminé. Les services devraient être en cours d'exécution."
    }
  }
}
