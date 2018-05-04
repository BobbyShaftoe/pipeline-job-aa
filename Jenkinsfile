@Library("PipelineLibrary") _

node('aws-node-00') {
  stage('Retrieve scm vars') {
    def checkoutVars = checkout scm
    def commit_id = checkoutVars.GIT_COMMIT
  }
}

//message={GIT_BRANCH=origin/master
// GIT_COMMIT=9662771cb3c37c7d8586500fac4e0f58d5b10514
// GIT_LOCAL_BRANCH=master
// GIT_PREVIOUS_COMMIT=e71c0191e6bf071f6f910e963b143ae635c94928
// GIT_PREVIOUS_SUCCESSFUL_COMMIT=f76fcbc7c585d76fe897d1e7da8153bf7041753b
// GIT_URL=https://github.com/BobbyShaftoe/pipeline-job-aa.git



setupCheck {
}


node('aws-node-00') {
  ansiColor('xterm') {
      environment {
        JOB_DEFINITION = 'Test'
      }

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

