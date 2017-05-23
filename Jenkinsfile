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
        parallel(
          "PHPUnit": {
            dir(path: 'blog') {
              sh './vendor/bin/phpunit'
            }
            
            
          },
          "PHPCD": {
            dir(path: 'blog') {
              sh './vendor/phpcd'
            }
            
            
          }
        )
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploy'
      }
    }
  }
}