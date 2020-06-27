node {

  stage ('Checkout from SCM') {
  
        checkout scm
      
  }
  
  stage ('list pods from kube-system') {
    withKubeConfig([credentialsId: 'kubeconfig' serverUrl: 'https://BA1F851E46F910C2BBF1ABB9CFCB20EE.gr7.us-west-2.eks.amazonaws.com']) {
     sh 'kubectl -n kube-system get pods'
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


  
