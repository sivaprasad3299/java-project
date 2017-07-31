pipeline {
  agent none
  stages {
    stage('unit test') {
      agent {
        label 'apache'
      }
      steps{
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
    }
    stage('build') {
      agent {
        label 'apache'
      }
      steps {
        sh 'ant -f build.xml -v'
      }
      post {
        success {
          archiveArtifacts artifacts:  'dist/*.jar', fingerprint: true
        }
      }
    }
    stage('deploy') {
      agent {
        label 'apache'
      }
      steps {
        sh "mkdir /var/www/html/rectangles/all/${env.BRANCH_NAME}"
        sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/${env.BRANCH_NAME}"
      }
    }
    stage('running on CentOS') {
      agent {
        label 'CentOS'
      }
      steps {
        sh "wget http://siva4devops1.mylabserver.com/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      }
    }
    stage('running on docker') {
      agent {
        docker 'openjdk:8u121-jre'
      }
      steps {
        sh "wget http://siva4devops1.mylabserver.com/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 7 8"
      }
    }
    stage('Promote to Green') {
      agent {
        label 'apache'
      }
      when {
        branch 'master'
      }
      steps{
        sh "cp /var/www/html/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/green/rectangle_${env.BUILD_NUMBER}.jar"
      }
    }
  }
}
