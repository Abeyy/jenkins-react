pipeline {
  agent {
    docker {
      image 'node:6-alpine' 
      args '-p 3000:3000' 
    }
  }
  options {
      timeout(time: 2, unit: 'MINUTES') 
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        sh 'npm run build'
      }
    }
    stage('Deploy to s3') {
      when {
        branch 'main'
      }
      steps {
        echo 'Deploying to AWS s3 bucket.'
        withAWS(region:'us-west-2', credentials:'aws-creds') {
          s3Delete(bucket: 'jenkins-react', path:'/')
          s3Upload(bucket: 'jenkins-react', path: "", includePathPattern: '**/*', workingDir: '/Users/abeyjoy/projects/jenkins-react/build')
        }
      }
    }
  }
}