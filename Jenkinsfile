#!/usr/bin/env groovy

stage("Trigger Orchestrator") {
 jobMap = [:]
 jobMap["job"] = "../../kubernetes-test-orchestrator/master"
 build jobMap
 echo "Changes with Orchestrator and Executor new"
}
