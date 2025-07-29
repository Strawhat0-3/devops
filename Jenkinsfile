pipeline {
  agent any

  environment {
    VOTE_PORT = '5000'
    RESULT_PORT = '5001'
    DOCKER_BUILDKIT = '1' // Active buildkit pour optimiser les builds Docker
  }

  stages {
    stage('Check Tools') {
      steps {
        sh '''
          echo "=== Vérification Docker & Docker Compose ==="
          docker --version || { echo " Docker introuvable"; exit 1; }
          docker compose version || docker-compose --version || { echo " Docker Compose introuvable"; exit 1; }
        '''
      }
    }

    stage('Cloner le dépôt') {
      steps {
        git branch: 'main', url: 'https://github.com/Strawhat0-3/devops'
      }
    }

    stage('Build des images Docker') {
      steps {
        // Utilisation de --pull pour mettre à jour sans re-télécharger tout
        sh 'docker compose build --pull'
      }
    }

    stage('Lancer l’application') {
      steps {
        sh 'docker compose up -d'
      }
    }

    stage('Vérification des services') {
      steps {
        sh 'docker compose ps'
        sh 'docker ps'
      }
    }
  }

  post {
    always {
      echo " Pipeline terminé. Les services devraient être en cours d'exécution."
    }
    failure {
      echo " Erreur détectée dans le pipeline."
    }
  }
}
