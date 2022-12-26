pipeline {
  agent any
  stages {
    stage('Deploy to s3') {
      when {
        branch 'main'
      }
      steps {
        echo 'Deploying to AWS s3 bucket.'
        withAWS(region:'us-east-1', credentials:'aws-creds') {
          s3Delete(bucket: 'jenkins-react', path:'**/*')
          s3Upload(bucket: 'jenkins-react', includePathPattern:'**/*')
        }
      }
    }
  }
}