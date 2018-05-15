@Library('jenkins-library') _

pipeline {
  agent none

  environment {
    NODE_VER = '8.1.0'
  }

  stages {
    stage('Beginning') {
      agent any
      environment {
        BEG_STG_VAR = 'Hey, we are beginning!'
      }
      steps {
        echo 'Hello World'
        sh 'echo $NODE_VER'
        echo "${env.BEG_STG_VAR}"
      }
    }

    stage('Who Am I?') {
      agent any
      environment {
        WHOAMI_VAR = 'I am printing'
      }
      steps {
        echo "${env.WHOAMI_VAR}"
        sh 'host -t TXT pgp.michaelholley.us |awk -F \'"\' \'{print $2}\''
      }
    }

    stage('Deploy to stage?') {
      agent none
      when {
        branch 'stage'
      }
      steps {
        input 'Ready to deploy to stage?'
      }
    }

    stage('Parallel Build') {
      failFast true
      parallel {
        stage('Stage One') {
          agent any
          steps {
            echo "1 - Stage one executing"
          }
        }

        stage('Stage Two') {
          agent any
          steps {
            echo "2 - Stage two executing"
          }
        }

        stage('Stage Three') {
          agent any
          steps {
            echo "3 - Stage three executing"
          }
        }
      }
    }
  }
}
