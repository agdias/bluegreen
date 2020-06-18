node {

  stage ('Checkout from SCM') {
  
        checkout scm
      
  }
  
  stage ('Lint HTML') {
    sh 'tidy -q -e app/*.html'
  }
  
  stage ('Build and push docker image') {
  
    def customImage = docker.build 'angelodias/bluegreen:${env.BRANCH}'
       docker.withRegistry('https://registry-1.docker.io/v2/','dockerhub') {
          customImage.push()
          
      }
  }
 
}


  
