pipeline {
  agent any

  environment {
    VOTE_PORT = '5000'
    RESULT_PORT = '5001'
  }

  stages {
    stage('Cloner le dépôt') {
      steps {
        git url: 'https://github.com/Strawhat0-3/devops'
      }
    }

    stage('Build des images Docker') {
      steps {
        sh 'docker-compose build'
      }
    }

    stage('Lancer l’application') {
      steps {
        sh 'docker-compose up -d'
      }
    }

    stage('Vérification des services') {
      steps {
        sh 'docker-compose ps'
        sh 'docker ps'
      }
    }
  }

  post {
    always {
      echo "Pipeline terminé. Les services devraient être en cours d'exécution."
    }
  }
}
