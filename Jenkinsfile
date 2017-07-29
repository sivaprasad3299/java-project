pipeline {
  agent any

  stages {
    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
        sh 'cd dist'
        sh 'java -jar rectangle.jar 4 5'
      }
    }
  }
}
