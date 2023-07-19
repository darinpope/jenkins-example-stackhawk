pipeline {
  agent { label "linux" } 
  environment {
    STACKHAWK_API_KEY = credentials("stackhawk-api-key")
  }
  stages {
    stage("Deploy site") {
      steps {
        sh 'sudo cp index.json /var/www/html'
      }
    }
    stage("Run HawkScan Test") {
      steps {
        sh '''
          docker run -v ${WORKSPACE}:/hawk:rw -t \
            -e API_KEY=${STACKHAWK_API_KEY} \
            -e NO_COLOR=true \
            stackhawk/hawkscan
        '''        
      }
    }
  }
}
