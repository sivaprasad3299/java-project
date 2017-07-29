pipeline {
  agent any

  stages {
    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
        sh 'java -jar rectangle.jar 4 5'
      }
    }
  }
}
