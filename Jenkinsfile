pipeline {
  agent any
  stages {
    stage ('GetEnv') {
      steps {
        sh 'printenv'
      }
    }
    
     stage ('Publish to ECR') {
      steps {
        withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
          sh 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/v3q1f7h3' 
          sh 'docker build -t test-demo .'
          sh 'docker tag test-demo:latest public.ecr.aws/v3q1f7h3/test-demo:""$BUILD_ID""'
          sh 'docker push public.ecr.aws/v3q1f7h3/test-demo:""$BUILD_ID""'
         }
       }
     }
  }
}
