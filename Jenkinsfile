#!/usr/bin/env groovy
def cloudDockerRegistryCredentialsId = '24cb9b3a-f0c3-4e12-b5dc-bfeead404fba'

node('docker-xlarge') {
 stage ("SetUp") {
    def scmVars = checkout scm
    branchName = "${scmVars.GIT_BRANCH}"
    currentBuild.displayName = "${branchName}-${env.BUILD_NUMBER}"

    withCredentials([usernamePassword(credentialsId: cloudDockerRegistryCredentialsId,
    passwordVariable: 'CLOUD_DOCKER_REGISTRY_PASSWORD',
    usernameVariable: 'CLOUD_DOCKER_REGISTRY_USER')]) {
    echo "******************"
    sh "env"
    sh "docker rmi -f mywebimage"
    sh "docker build --no-cache -t mywebimage ."
   sh "docker login https://cirrus.jfrog.io/cirrus -u=${CLOUD_DOCKER_REGISTRY_USER} -p=${CLOUD_DOCKER_REGISTRY_PASSWORD}"
    sh "docker tag mywebimage:latest cirrus-docker.jfrog.io/github-pega-web"
    sh "docker push cirrus-docker.jfrog.io/github-pega-web"
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
