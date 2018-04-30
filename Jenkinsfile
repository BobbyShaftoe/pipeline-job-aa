@Library("PipelineLibrary") _
import import org.aws.*

    setupCheck {
}

pipeline {
  agent any

  environment {
    JOB_DEFINITION = 'Test'
  }


  stages {

    stage('Run the env script') {
      steps {
        sh 'python scripts/env_info_helper.py env_var HOME'
      }
    }

    stage('Generate AWS VARS from meta-data') {
        steps {
          script {
            awsDetails = getAWSDetails()
            AZ = awsDetails['az']
            REGION = awsDetails['region']
            ACCOUNT = awsDetails['account']
            ECR = awsDetails['ecr']
            CLI_IMAGE = "${ECR}/${REPO_NAMESPACE}/cli:latest"
          }
          sh "env"
        }
      }

  }

}

