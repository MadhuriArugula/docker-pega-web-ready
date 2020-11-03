pipeline {
  agent any
  stages {
    stage('Stage 1') {
      steps {
        echo 'Setting up cloud clusters'
        echo ' Init!!!!'
        sleep 60
      }
    }
     stage('Stage 2') {
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
