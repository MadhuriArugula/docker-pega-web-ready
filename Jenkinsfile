pipeline {
  agent any
  stages {
    stage('Setup') {
      steps {
        echo 'Setting up cloud clusters'
        echo ' Init!!!!'
         pullRequest.labels.each{
             echo "label: $it"
          }
      }
    }
     stage('Deploy') {
      steps {
        echo ' Deploying charts and building images'
        
      }
    }

    stage('Tests') {
      steps {
        echo 'Running Tests!!'
        
      }
    }
  }
}
