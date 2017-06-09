pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'composer install'
        sh '''cp .env.example .env
'''
        sh 'php artisan key:generate'
      }
    }
    stage('Lauch test') {
      steps {
        sh './vendor/bin/phpunit'
      }
    }
    stage('Deploy') {
      steps {
        sh 'rocketeer deploy --host="192.168.32.10" --password="6fe7b5d4f79c9ddd94b4a8f7" --key="" --repository="https://github.com/ygout/blogLaravel.git" --branch="master"'
        sh 'php artisan cache:clear'
      }
    }
  }
  triggers {
    pollSCM('* * * * *')
  }
}