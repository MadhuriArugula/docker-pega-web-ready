#!/usr/bin/env groovy

def labels = ""
def imageName = ""
node {

  stage("Initialze"){
      if (env.CHANGE_ID) {
        pullRequest.labels.each{
        echo "label: $it"
        validateProviderLabel(it)
        labels += "$it,"
      }
        labels = labels.substring(0,labels.length())
        echo "PR labels -> $labels"
     }else {
       currentBuild.result = 'ABORTED'
       throw new Exception("Aborting as this is not a PR job")
     }
 }
  
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
      }
  }

  stage("Trigger Orchestrator") {
    jobMap = [:]
    jobMap["job"] = "../kubernetes-test-orchestrator/US-366319"
    jobMap["parameters"] = [
                            string(name: 'PROVIDER', value: labels),
                            string(name: 'WEB_IMAGE_NAME', value: imageName),
                        ]
    jobMap["propagate"] = true
    jobMap["quietPeriod"] = 0 
    resultWrapper = build jobMap
    currentBuild.result = resultWrapper.result
 } 

}

def validateProviderLabel(String provider){
    def validProviders = ["integ-all","integ-eks","integ-gke","integ-aks"]
    if(!validProviders.contains(provider)){
        currentBuild.result = 'FAILURE'
        pullRequest.comment("Invalid provider label - ${provider}. valid labels are ${validProviders}")
        throw new Exception("Invalid provider label - ${provider}. valid labels are ${validProviders}")
    }
}
