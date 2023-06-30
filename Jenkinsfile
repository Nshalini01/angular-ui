pipeline {
  agent {
    label 'jenkins'
  }
  stages {
    stage('install') {
      steps{
        sh "npm install"
      }
    }

    stage('build') {
      steps{
        sh "npm run build"
      }
    }

    stage('deploy') {
      steps {
        sh "npm run deploy"
      }
    }
  }
}
