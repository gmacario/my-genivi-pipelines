pipeline {
  agent {
    docker {
      image 'httpd:2.2.32'
    }
    
  }
  stages {
    stage('Build Quick') {
      steps {
        echo 'Starting Build'
        sh 'echo TODO: mvn clean install -DskipTests'
        // node(label: 'windows') {
        //   sh 'call doATest.bat'
        // }
        
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Chrome": {
            echo 'testing in chrome'
            sh 'echo TODO: mvn test -Dbrowser=chrome'
            
          },
          "Firefox": {
            echo 'testing in firefox'
            sh 'echo TODO: mvn test -Dbrowser=firefox'
            
          }
        )
      }
    }
    stage('Deploy') {
      steps {
        echo 'deploying'
      }
    }
  }
  environment {
    USER = 'apache'
    HOME_FOLDER = '/var/www'
  }
}
