pipeline {
  agent any
  stages {
    stage('First stage') {
      steps {
        echo 'Setting up cloud clusters'
        echo ' Init!!!!'
        sleep 60
      }
    }
     stage('Second stage') {
      steps {
        echo ' Deploying charts and building images'
        sleep 30
      }
    }

    stage('Third stage') {
      steps {
        echo 'Running Tests!!'
        sleep 30
      }
    }
  }
}
