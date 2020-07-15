#!/usr/bin/env groovy

node {
 stage ("Checkout and Build Images") {
    def scmVars = checkout scm
    branchName = "${scmVars.GIT_BRANCH}"
    currentBuild.displayName = "${branchName}-${env.BUILD_NUMBER}"
    imageName = "docker-dev.bin.pega.io/github:${env.BUILD_NUMBER}"
    withCredentials([usernamePassword(credentialsId: "bin.pega.io",
    passwordVariable: 'ARTIFACTORY_PASSWORD', usernameVariable: 'ARTIFACTORY_USER')]) {
    sh 'docker login -u ${ARTIFACTORY_USER} -p ${ARTIFACTORY_PASSWORD} docker-dev.bin.pega.io'
    sh "docker build --no-cache -t ${imageName} ."
    sh "docker push ${imageName}"
    sh "docker pull ${imageName}"
    sh "docker image ls"
  }
//   if (env.CHANGE_ID) {
//          pullRequest.labels.each{
//             echo "label: $it"
//          }
//      }
 }
 stage("Trigger Orchestrator") {
  jobMap = [:]
  jobMap["job"] = "../kubernetes-test-orchestrator/master"
  build jobMap
  echo "Changes with Orchestrator and Executor new"
  echo "New line"
 } 
}
