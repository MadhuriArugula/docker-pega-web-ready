#!/usr/bin/env groovy

node {
 stage ("SetUp") {
    def scmVars = checkout scm
    branchName = "${scmVars.GIT_BRANCH}"
    currentBuild.displayName = "${branchName}-${env.BUILD_NUMBER}"

    withCredentials([usernamePassword(credentialsId: cloudDockerRegistryCredentialsId,
    passwordVariable: 'CLOUD_DOCKER_REGISTRY_PASSWORD',
    usernameVariable: 'CLOUD_DOCKER_REGISTRY_USER')]) {
    sh "docker build -t mywebimage ."
    sh "docker login -u=${CLOUD_DOCKER_REGISTRY_USER} -p=${CLOUD_DOCKER_REGISTRY_PASSWORD}"
    sh "docker tag mywebimage:latest github/pegaweb"
    sh "docker images"
    sh "docker push github/pegaweb"
    sh "docker logout"
  }
 }
 stage("Trigger Orchestrator") {
  jobMap = [:]
  jobMap["job"] = "../../kubernetes-test-orchestrator/master"
  build jobMap
  echo "Changes with Orchestrator and Executor new"
  echo "New line"
 }
}
