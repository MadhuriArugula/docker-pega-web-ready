#!/usr/bin/env groovy

node {
 stage ("SetUp") {
    def scmVars = checkout scm
    branchName = "${scmVars.GIT_BRANCH}"
    currentBuild.displayName = "${branchName}-${env.BUILD_NUMBER}"

    withCredentials([usernamePassword(credentialsId: cloudDockerRegistryCredentialsId,
    passwordVariable: 'CLOUD_DOCKER_REGISTRY_PASSWORD',
    usernameVariable: 'CLOUD_DOCKER_REGISTRY_USER')]) {
    docker build -t mywebimage .
    docker login -u=${CLOUD_DOCKER_REGISTRY_USER} -p=${CLOUD_DOCKER_REGISTRY_PASSWORD}
    docker tag mywebimage:latest github/pegaweb
    docker images
    docker push github/pegaweb
    docker logout
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
