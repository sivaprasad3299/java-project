pipeline {
  agent any

  stages {
    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
      }
    }
  }

  post {
    always {
      archiveArticats artifacts:  'dist/*.jar', fingerprint: true
    }
  }
}
