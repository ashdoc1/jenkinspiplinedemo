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
          ls -lrt
          docker ls
        }
      }
      stage('Back-end') {
            agent {
                docker { image 'maven:3-alpine' }
            }
            steps {
                echo "pwd: " pwd
                sh 'mvn --version'
            }
        }
        stage('Front-end') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'node --version'
            }
        }
    }
}
