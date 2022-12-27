pipeline {
  agent {
    docker {
      image 'node:12-alpine' 
      args '-u root:root'
    }
  }
  options {
      timeout(time: 15, unit: 'MINUTES') 
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
          s3Upload(bucket: 'jenkins-react', path: "", includePathPattern: '**/*', workingDir: '/build')
        }
      }
    }
  }
}