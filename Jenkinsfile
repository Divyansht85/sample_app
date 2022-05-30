pipeline {
  agent any
  stages {
      stage('Test') {
      agent any
      steps {
        sh "echo 'Testing 9'"
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
    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "sample-app-definition.yaml", kubeconfigId: "kubernetes")
        }
      }
    }
  }
}
