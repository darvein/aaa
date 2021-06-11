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
          sh 'ping google.com -c 2 | tee -a output.txt'
          sh 'printenv | tee -a output.txt'
          sh 'echo "This is the branch: $BRANCH_NAME"'
          sh '''
          curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, World!"}' https://hooks.slack.com/services/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
          '''
      }
    }

  post {
    success {
      archiveArtifacts artifacts: 'output.txt'
      cleanWs()
    }
  }
}
