pipeline {
  agent any
  stages {
    stage('first') {
      steps {
        echo 'PRs from same repository working!!'
        echo ' In First stage'
        //sleep 120
        //  error "Failing it .........."

      }
    }
     stage('second') {
      steps {
        echo 'hello there!!'
        echo ' In second stage'
        echo ' Hey!! Change from different branch'

      }
    }

    stage('third') {
      steps {
        echo 'In Third stage'
      }
    }
  }
}
