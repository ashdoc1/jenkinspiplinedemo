pipeline {
  agent any
  environment {
    RELEASE='20.04'
  }
    stages {
      stage('one') {    
        steps {
          echo 'hello, this is stage one'
        }
      }
      stage('Verify Branch') {
        environment {
          LOG_LEVEL='INFO'

        }
        steps {
          echo "GIT_BRANCH: $GIT_BRANCH"
          echo "WORKSPACE: $WORKSPACE"
          echo "log level is $LOG_LEVEL"
        }
      }
      stage('deploy') {
        input {
          message 'deploy it?'
          ok 'do it'
          parameters{
            string (name: 'TARGET_ENVIRONMENT', defaultValue: 'PROD', description: 'Target deployment Environment')
          }
          steps {
            echo "deploying release to ${RELEASE} to environment ${TARGET_ENVIRONMENT}"
          }
        }
      }
      stage('Back-end') {
				agent {
						docker { image 'nginx' }
				}
				steps {
					sh 'node --version'
				}
      }
    }
}
