@Library("PipelineLibrary") _
  setupCheck {
}

buildInfo()






node('aws-node-00') {

  environment {
    JOB_DEFINITION = 'Test'
  }

  try {

  stage('Run the env script') {
    sh 'python scripts/env_info_helper.py env_var HOME'
  }

  } catch (err) {
    currentBuild.result = 'FAILED'
    throw err
  }
}

