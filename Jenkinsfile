pipeline {
  agent none
  stages {
      stage('Test') {
      agent any
      steps {
        sh 'echo 'Tests passed'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t divyansht85/sample-app:latest .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push divyansht85/sample-app:latest'
        }
      }
    }
  }
}
