pipeline {
  agent any
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
stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    echo 'Scanning'
                    sh 'sonar:sonar'
                }
            }
        }
        
        stage("Quality Gate") {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'MINUTES') {
                            def qualityGate = waitForQualityGate abortPipeline: true
                            echo "Quality Gate status is ${qualityGate.status}"
                            echo "Quality Gate details: ${qualityGate}"
                        }
                    } catch (Exception e) {
                        echo "Quality Gate failed: ${e.getMessage()}"
                    }
                }
            }
        }
    stage('deploy') {
      steps {
        sh "npm run deploy"
      }
    }
  }
}
