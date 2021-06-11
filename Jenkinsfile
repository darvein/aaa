pipeline {
  agent {
    label 'slave'
  }

  tools {
    nodejs 'node14'
    dockerTool 'docker'
  }

  options {
    throttleJobProperty(
        categories: ['throttle'],
        throttleEnabled: true,
        throttleOption: 'category',
    )
  }

    stages {
      stage('Hello') {
        steps {
          echo 'Hello World'
        }
      }

      stage('Server') {
        steps {
          sh 'sleep 120'
          sh 'hostname'
          sh 'pwd'
        }
      }

      stage('Build') {
        steps {
          sh 'npm install'
          sh 'docker ps'
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
        slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }

    failure {
      slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }

    always {
    }
  }
}
