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
          sh 'docker login -u AWS -p $(aws ecr get-login-password --region us-east-) public.ecr.aws/v3q1f7h3' 
          sh 'docker build -t agency .'
          sh 'docker tag betaemission:latest 275254035816.dkr.ecr.us-east-2.amazonaws.com/betaemission:""$BUILD_ID""'
          sh 'docker push 275254035816.dkr.ecr.us-east-2.amazonaws.com/betaemissio:""$BUILD_ID""'
         }
       }
     }
  }
}

