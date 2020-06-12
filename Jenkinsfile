pipeline {
  agent any
  stages {
    stage('Setup') {
      steps {
        echo 'Setting up EKS cloud cluster'
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
        echo ' Running EKS Tests!!'
        sleep 30
      }
    }
  }
}
