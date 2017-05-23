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
          sh 'php artisan key:generate'
        }
        
      }
    }
  }
}