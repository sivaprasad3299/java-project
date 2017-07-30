pipeline {
  agent any

  options {
    buildDiscarded(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))  
  }
  stages {
    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts:  'dist/*.jar', fingerprint: true
    }
  }
}
