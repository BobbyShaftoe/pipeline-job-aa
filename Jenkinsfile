
node ('master') {
    stage('Checkout main repository') {
      git poll: false, url: 'https://github.com/BobbyShaftoe/pipeline-job-aa.git'
    }

    stage('List files in workspace') {
      sh 'ls -larst .'
      sh 'ls -la */*'
    }

    stage('Environment') {
       sh 'scripts/env.sh' 
            
    }
    stage('Read placeholder') {
      readFile 'lib/placeholder.txt'
    }
}

