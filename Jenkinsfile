@Library("PipelineLibrary") _
  setupCheck {
}


node('aws-node-00') {

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
    ECR = awsDetails['ecr']
    CLI_IMAGE = "${ECR}/${REPO_NAMESPACE}/cli:latest"

    sh "env"
  }




  } catch (err) {
    currentBuild.result = 'FAILED'
    throw err
  }
}

