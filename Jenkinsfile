pipeline {
  agent any
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
      stage('Back-end') {
				agent {
						docker { image 'nginx' }
				}
				stages {
						stage('Test') {
								steps {
										sh 'node --version'
								}
						}
				}
      }
    }
}
