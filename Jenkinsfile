pipeline {
  agent any
  stages {
    stage('Setup') {
      steps {
        echo 'Setting up EKS cloud cluster'
        echo ' Setting up'
        sleep 10
      }
    }
     stage('Deploy') {
      steps {
        echo ' Deploying charts and building images'
        sleep 10
      }
    }

    stage('Tests') {
      steps {
        echo 'Running Tests!!'
        echo ' Running EKS Tests!!'
        sleep 10
      }
    }
  }
}
