pipeline {
  agent any
  options {
      timeout(time: 2, unit: 'MINUTES') 
  }
  stages {
    stage('Deploy to s3') {
      when {
        branch 'main'
      }
      steps {
        echo 'Deploying to AWS s3 bucket.'
        withAWS(region:'us-west-2', credentials:'aws-creds') {
          s3Delete(bucket: 'jenkins-react', path:'/')
          s3Upload(bucket: 'jenkins-react', path: "jobs/$JOB_NAME/$BUILD_NUMBER/", includePathPattern: '*', workingDir: '/Users/abeyjoy/projects/jenkins-react/build')
        }
      }
    }
  }
}