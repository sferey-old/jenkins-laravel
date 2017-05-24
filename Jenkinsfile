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
          "Report": {
            publishHTML(target: 'publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: \'coverage\', reportFiles: \'index.html\', reportName: \'HTML Report\', reportTitles: \'RCov Report\'])')
            
          }
        )
      }
    }
  }
}