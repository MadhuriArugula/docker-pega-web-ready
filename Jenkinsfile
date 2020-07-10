#!/usr/bin/env groovy

node {
 stage ("SetUp") {
  checkout scm
 }
 stage("Trigger Orchestrator") {
  jobMap = [:]
  jobMap["job"] = "../../kubernetes-test-orchestrator/master"
  build jobMap
  echo "Changes with Orchestrator and Executor new"
  echo "New line"
 }
}
