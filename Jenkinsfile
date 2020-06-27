node {

  stage ('Checkout from SCM') {
  
        checkout scm
      
  }
  
  stage ('list pods from kube-system') {
     withAWS(credentials: 'aws-static',
             region: 'us-west-2') {
        sh '''
          kubectl -n kube-system get pods
           '''
     }
  }
  
  stage ('Lint HTML') {
    sh 'tidy -q -e app/*.html'
  }
  
  stage ('Build and push docker image') {
  
    def customImage = docker.build 'angelodias/bluegreen:latest'
       docker.withRegistry('https://registry-1.docker.io/v2/','dockerhub') {
          customImage.push()
          
      }
  }
 
}


  
