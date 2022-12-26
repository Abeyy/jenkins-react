pipeline {
  agent any
  stages {
    stage('Deploy to s3') {
      when {
        branch 'main'
      }
      steps {
        echo 'Deploying to AWS s3 bucket.'
        withAWS(region:'us-west-2', credentials:'AKIAZD33PCQSDBWEIU4A') {
          s3Delete(bucket: 'jenkins-react', path:'**/*')
          s3Upload(bucket: 'jenkins-react', includePathPattern:'**/*')
        }
      }
    }
  }
}