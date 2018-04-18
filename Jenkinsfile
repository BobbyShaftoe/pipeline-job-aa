
node master {
    stage('Environemnt') {
       sh 'scripts/env.sh' 
            
    }
    stage('Read placeholder') {
      readFile 'lib/placeholder.txt'
    }
}

