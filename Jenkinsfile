#!/usr/bin/env groovy
def cloudDockerRegistryCredentialsId = '24cb9b3a-f0c3-4e12-b5dc-bfeead404fba'

node {
 stage ("Checkout and Build Images") {
    def scmVars = checkout scm
    branchName = "${scmVars.GIT_BRANCH}"
    currentBuild.displayName = "${branchName}-${env.BUILD_NUMBER}"
    withCredentials([usernamePassword(credentialsId: cloudDockerRegistryCredentialsId,
    passwordVariable: 'CLOUD_DOCKER_REGISTRY_PASSWORD',
    usernameVariable: 'CLOUD_DOCKER_REGISTRY_USER')]) {
    sh "docker rmi -f pega-web-ready"
    sh "docker build --no-cache -t pega-web-ready ."
    sh "docker login cirrus-docker.jfrog.io -u=${CLOUD_DOCKER_REGISTRY_USER} -p=${CLOUD_DOCKER_REGISTRY_PASSWORD}"
    sh "docker tag pega-web-ready:latest cirrus-docker.jfrog.io/github-web-ready:${env.BUILD_NUMBER}"
    sh "docker push cirrus-docker.jfrog.io/github-web-ready:${env.BUILD_NUMBER}"
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
