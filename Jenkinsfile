pipeline {
  agent any
  stages {
    stage ('GetEnv') {
      steps {
        sh 'printenv'
      }
    }
        // Publish to Prublic ECR REPO

     stage ('Publish to ECR') {
      steps {
        withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
          sh 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/v3q1f7h3' 
          sh 'docker build -t repo .'
          sh 'docker tag repo:latest public.ecr.aws/v3q1f7h3/repo:""$BUILD_ID""'
          sh 'docker push public.ecr.aws/v3q1f7h3/repo:""$BUILD_ID""'
         }
       }
     }

    //  Publish to Private ECR REPO
    //  stage ('Publish to ECR') {
    //   steps {
    //     withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
    //       sh 'docker login -u AWS -p $(aws ecr get-login-password --region us-east-1) 275254035816.dkr.ecr.us-east-2.amazonaws.com' 
    //       sh 'docker build -t private .'
    //       sh 'docker tag private:latest 275254035816.dkr.ecr.us-east-2.amazonaws.com/private:""$BUILD_ID""'
    //       sh 'docker push 275254035816.dkr.ecr.us-east-2.amazonaws.com/private:""$BUILD_ID""'
    //      }
    //    }
    //  }
  }
}


// aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/v3q1f7h3

// docker tag private:latest 275254035816.dkr.ecr.us-east-2.amazonaws.com/private:latest
// docker push 275254035816.dkr.ecr.us-east-2.amazonaws.com/private:latest


