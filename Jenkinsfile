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
          echo "$GIT_BRANCH"
        }
      }
    }
}
