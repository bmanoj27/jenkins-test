pipeline {
  triggers {
    cron ('H/5 * * * *')
  }
  agent {
    node {
      label 'nodejs'
    }
  }
  stages {
    stage ('Creating a new redis application') {
      steps {
        sh 'oc new-app --name redis docker.io/shady4u/redis'
      }
    }
  }
  post {
    failure {
      echo 'FAILED'
      sh 'oc status'
    }
    success {
      sh 'oc expose service redis'
      sh 'oc status'
      sh 'oc get all'
      echo 'SUCCESS'
    }
  }
}
