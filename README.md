### Getting Started

## Create AWS ECR
https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-console.html

Create a private ECR(awscodebuild-demo) and copy it's URI. 

It will be something like the one below.
736094578720.dkr.ecr.us-east-1.amazonaws.com/awscodebuild-demo


## Configure AWS CLI
aws configure

aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 736094578720.dkr.ecr.us-east-1.amazonaws.com

docker build -t awscodebuild-demo .

docker tag awscodebuild-demo:latest 736094578720.dkr.ecr.us-east-1.amazonaws.com/awscodebuild-demo:latest

docker push 736094578720.dkr.ecr.us-east-1.amazonaws.com/awscodebuild-demo:latest

Verify that docker image is listed under this ECR instance

