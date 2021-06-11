pipeline {
  agent {
    label 'slave'
  }

  tools {
    nodejs 'node14'
    docker 'docker'
  }

    stages {
      stage('Hello') {
        steps {
          echo 'Hello World'
        }
      }

      stage('Server') {
        steps {
          sh 'hostname'
          sh 'pwd'
        }
      }

      stage('Build') {
        steps {
          sh 'npm install'
        }
      }

      stage('Bye'){
        environment {
          SECRET = credentials('secret-token')
        }

        steps {
          sh 'ping google.com -c 2 | tee -a output.txt'
          sh 'printenv | tee -a output.txt'
          sh 'echo "This is the branch: $BRANCH_NAME"'
          sh 'echo "This is the secret: $SECRET" | tee output.txt'
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
