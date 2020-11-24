pipeline {
  agent any
  stages {
    stage('Test stage1') {
      steps {
        echo 'Setting up cloud clusters'
        echo ' Init!!!!'
        sleep 60
      }
    }
     stage('Test Stage 2') {
      steps {
        echo ' Deploying charts and building images'
        sleep 30
      }
    }

    stage('Test Stage3') {
      steps {
        echo 'Running Tests!!'
        sleep 30
      }
    }
  }
}
