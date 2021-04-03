pipeline {
  agent any
    stages {
      stage('one') {    
        steps {
          echo 'hello, this is stage one'
        }
      }
      stage('Verify Branch') {
        steps {
          echo "GIT_BRANCH: $GIT_BRANCH"
          echo "WORKSPACE: $WORKSPACE"
        }
      }
      stage('Back-end') {
				agent {
						docker { image 'node:14-alpine' }
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
