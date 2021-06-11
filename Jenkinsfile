pipeline {
  agent any

    stages {
      stage('Hello') {
        steps {
          echo 'Hello World'
        }
      }

      stage('Bye'){
        steps {
          sh 'ping google.com -c 20 | tee -a output.txt'
          sh 'printenv | tee -a output.txt'
        }
      }
    }

  post {
    success {
      archiveArtifacts artifacts: 'output.txt'
      cleanWs()
    }
  }
}
