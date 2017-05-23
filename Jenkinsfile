pipeline {
  agent any
  stages {
    stage('Echo') {
      steps {
        echo 'Hello World'
      }
    }
    stage('Build') {
      steps {
        dir(path: 'blog') {
          sh 'composer install'
          sh 'cp .env.example .env'
          sh 'php artisan key:generate'
        }
        
      }
    }
    stage('UnitTest') {
      steps {
        dir(path: 'blog') {
          sh './vendor/bin/phpunit'
        }
        
      }
    }
  }
}