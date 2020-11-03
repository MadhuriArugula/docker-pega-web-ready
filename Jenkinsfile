pipeline {
  agent any
  stages {
    stage('First Stage 1') {
      steps {
        echo 'Setting up cloud clusters'
        echo ' Init!!!!'
        sleep 60
      }
    }
     stage('Second Stage 2') {
      steps {
        echo ' Deploying charts and building images'
        sleep 30
      }
    }

    stage('Third stage 3') {
      steps {
        echo 'Running Tests!!'
        sleep 30
      }
    }
  }
}
