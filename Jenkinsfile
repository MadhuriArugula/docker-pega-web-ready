#!/usr/bin/env groovy
def cloudDockerRegistryCredentialsId = '24cb9b3a-f0c3-4e12-b5dc-bfeead404fba'

node {
 stage ("Checkout and Build Images") {
    def scmVars = checkout scm
    branchName = "${scmVars.GIT_BRANCH}"
    currentBuild.displayName = "${branchName}-${env.BUILD_NUMBER}"
    imageName = "cirrus-docker.jfrog.io/github-web-ready:${env.BUILD_NUMBER}"
    withCredentials([usernamePassword(credentialsId: cloudDockerRegistryCredentialsId,
    passwordVariable: 'CLOUD_DOCKER_REGISTRY_PASSWORD',
    usernameVariable: 'CLOUD_DOCKER_REGISTRY_USER')]) {
    sh "docker login cirrus-docker.jfrog.io -u=${CLOUD_DOCKER_REGISTRY_USER} -p=${CLOUD_DOCKER_REGISTRY_PASSWORD}"
    sh "docker build --no-cache -t ${imageName} ."
    sh "docker push ${imageName}"
  }
  Jenkins.instance.pluginManager.plugins.each{
    plugin -> 
    println ("${plugin.getDisplayName()} (${plugin.getShortName()}): ${plugin.getVersion()}")
    }
//   if (env.CHANGE_ID) {
//          pullRequest.labels.each{
//             echo "label: $it"
//          }
//      }
 }
 stage("Trigger Orchestrator") {
  jobMap = [:]
  jobMap["job"] = "../../kubernetes-test-orchestrator/master"
  build jobMap
  echo "Changes with Orchestrator and Executor new"
  echo "New line"
 } 
}
