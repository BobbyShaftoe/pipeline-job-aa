@Library("PipelineLibrary") _

checkoutVars = checkoutRepo {
}
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

