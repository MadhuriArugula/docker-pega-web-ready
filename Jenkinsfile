pipeline {
  agent any
  stages {
    stage('Setup') {
      steps {
        echo 'Setting up cloud clusters'
        echo ' Init!!!!'
        sleep 60
      }
    }
     stage('Deploy') {
      steps {
        echo ' Deploying charts and building images'
        sleep 30
      }
    }

    stage('Tests') {
      steps {
        echo 'Running Tests!!'
        sleep 30
      }
    }
  }
}
