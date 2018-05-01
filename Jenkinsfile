@Library("PipelineLibrary") _
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
        sh "env"
      }




      } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
      }
  }
}

