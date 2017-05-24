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
    stage('Test') {
      steps {
        dir(path: 'blog') {
          sh './vendor/bin/phpunit'
        }
        
      }
    }
    stage('Deploy') {
      steps {
        parallel(
          "Deploy": {
            echo 'Deploy'
            
          },
          echo 'Hello World'
        )
      }
    }
  }
}