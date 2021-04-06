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
      stage ('Build') {
          environment {
              LOG_LEVEL='INFO'
          }
          parallel {
              stage('linux-arm64') {
                  steps {
                      echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}..."
                      sh 'chmod +x scripts/build.sh'
                  }
              }
              stage('linux-amd64') {
                  steps {
                      echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}..."
                  }
              }
              stage('windows-amd64') {
                  steps {
                      echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}..."
                      sh pwd
                      sh 'chmod +x scripts/buid.sh'
                      withCredentials([string(credentialsId: 'API_KEY', variable: 'API_KEY')]){
                        sh  '''
                          ./scripts/build.sh
                        '''
                      }
                  }
              }
          }
      }
      stage ('deploy'){
        input {
          message 'Deploy?'
          ok 'do it!'
          parameters {
            string(name: 'TARGET_ENVIRONMENT', defaultValue: 'PROD', description: 'Target deployment environment')
          }
        }
        steps {
          echo "Deploying release ${RELEASE} to environment ${TARGET_ENVIRONMENT}"
        }
      }
      stage('Testing'){
        steps {
          echo "Testing release ${RELEASE}"
          writeFile file: 'test-results.txt', text: 'passed'       
        }
      }
    }
    post{
      always {
            echo 'Prints whether deploy happened or not, success or failure'
      }
      success {
         archiveArtifacts 'test-results.txt'
      }
    }
}
