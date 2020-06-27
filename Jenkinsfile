node {

  stage ('Checkout from SCM') {
  
        checkout scm
      
  }
  
  stage ('Lint HTML') {
    sh 'tidy -q -e app/*.html'
  }
  
  stage ('test kubernetes access') {
    withKubeConfig([credentialsId: 'k8s-token', serverUrl: 'http://apiserver.hallo.io:6443']) {
      sh 'kubectl apply -f blue.yaml'
    }
  }
  
  stage ('Build and push docker image') {
  
       def customImage = docker.build 'angelodias/bluegreen:blue'
       docker.withRegistry('https://registry-1.docker.io/v2/','dockerhub') {
          customImage.push()
          
      }
  }
 
}


  
