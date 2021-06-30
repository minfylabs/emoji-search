pipeline {
  environment {
    registry = "minfy/sample-app"
    registryCredential = 'dockerhub'
    KUBECONFIG="$JENKINS_HOME/.kube/config2"
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        sh "printenv"
        sh "docker build -t riteshk03/emoji-search:$BUILD_ID ."
       // sh "docker run -dp 80:80 riteshk03/emoji-search:$BUILD_ID"
        sh "docker push riteshk03/emoji-search:$BUILD_ID"
      }
    }
   

    stage('Creating Deployment') {
      steps {
        sh  '''
            kubectl set image deployment/my-app2.yaml httpd=riteshk03/emoji-search:$BUILD_ID
            '''
      }
    }

    stage('') {
      steps{
        sh '''
            kubectl get deployments
            kubectl get svc
            '''
      }
    }
    }
}
