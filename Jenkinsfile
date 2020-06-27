node {

  stage ('Checkout from SCM') {
  
        checkout scm
      
  }
  
  stage ('Lint HTML') {
    sh 'tidy -q -e app/*.html'
  }
  
  stage ('test kubernetes access') {
    withKubeConfig([credentialsId: 'kubeconfig', 
                    serverUrl: 'http://apiserver.hallo.io:6443',
                    namespace: 'kube-system'
                   ]) {
      sh 'kubectl get pods'
    }
  }
  
  stage ('Build and push docker image') {
  
       def customImage = docker.build 'angelodias/bluegreen:blue'
       docker.withRegistry('https://registry-1.docker.io/v2/','dockerhub') {
          customImage.push()
          
      }
  }
 
}


  
