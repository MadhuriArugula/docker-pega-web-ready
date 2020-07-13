#!/usr/bin/env groovy


node {
    stage('Build') {
        pullRequest.labels.each{
             echo "label: $it"
          }
    }
}
