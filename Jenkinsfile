
node {
    stage('List files in workspace') {
      sh 'ls -larst .'
      sh 'ls -la */*'
    }

    stage('Environemnt') {
       sh 'scripts/env.sh' 
            
    }
    stage('Read placeholder') {
      readFile 'lib/placeholder.txt'
    }
}

