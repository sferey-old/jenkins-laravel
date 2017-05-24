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
          "PHPMD": {
            dir(path: './blog') {
              sh './vendor/bin/phpmd ./app xml ../build/phpmd.xml --reportfile ../build/logs/pmd.xml'
            }
            
            
          }
        )
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploy'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: './build/logs', reportFiles: 'phpmd.xml', reportName: 'HTML Report', reportTitles: ''])
      }
    }
  }
}
