@Library("PipelineLibrary") _

node('aws-node-00') {
  stage('Retrieve scm vars') {
    def checkoutVars = checkout scm
    def commit_id = checkoutVars.GIT_COMMIT
    env.GIT_COMMIT = checkoutVars.GIT_COMMIT
    env.GIT_BRANCH = checkoutVars.GIT_BRANCH
    env.GIT_LOCAL_BRANCH = checkoutVars.GIT_LOCAL_BRANCH
    env.GIT_PREVIOUS_COMMIT = checkoutVars.GIT_PREVIOUS_COMMIT
    env.GIT_URL = checkoutVars.GIT_URL
  }

  stage('Checkout scm'){
    checkout scm
  }
}


setupCheck {
}


node('aws-node-00') {
  ansiColor('xterm') {
      environment {
        JOB_DEFINITION = 'Test'
      }
      echo "-------------------- Git Info --------------------"
      echo env.GIT_COMMIT
      echo env.GIT_BRANCH
      echo env.GIT_LOCAL_BRANCH
      echo env.GIT_PREVIOUS_COMMIT
      echo env.GIT_URL

      try {

      stage('Run the env script') {
        sh 'python scripts/env_info_helper.py env_var HOME'
      }

      stage('Generate AWS VARS from meta-data') {
        awsDetails = getAWSDetails()
        AZ = awsDetails['az']
        REGION = awsDetails['region']
        ACCOUNT = awsDetails['account']
        sh "echo AZ: $AZ"
        sh "echo REGION: $REGION"
        sh "echo ACCOUNT: $ACCOUNT"
      }

      } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
      }
  }
}

