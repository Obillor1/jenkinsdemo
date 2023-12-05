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
          sh 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-2) public.ecr.aws/t7e2c6o4' 
          sh 'docker build -t agency .'
          sh 'docker tag agency:latest 275254035816.dkr.ecr.us-east-2.amazonaws.com/betaemission:latest:""$BUILD_ID""'
          sh 'docker push 275254035816.dkr.ecr.us-east-2.amazonaws.com/agency:""$BUILD_ID""'
         }
       }
     }
  }
}

