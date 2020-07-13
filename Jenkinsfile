#!/usr/bin/env groovy


node {
    stage('Build') {
    	if (env.CHANGE_ID) {
        pullRequest.labels.each{
             echo "label: $it"
          }
        }
    }
}
