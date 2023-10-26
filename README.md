# Deploy Springboot Application to AWS ECR using GitHub Action
## Introduction
This is a sample project with simple springboot application. It is built and deployed to AWS ECR using GitHub action

Below are the high level steps:
- Triggers on commit to main branch
- [maven-build] Maven package build is invoked
- [maven-build] Application jar and docker files are uploaded to staging area
- [docker-build] Artifacts are downloaded from staging area
- [docker-build] Login to Amazon ECR 
- [docker-build] Build, tag, and push image to Amazon ECR

## Getting Started

### Create AWS ECR

https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-console.html

Create a private ECR(awscodebuild-demo) and copy it's URI.

It will be something like the one below.
[IMAGEID].dkr.ecr.us-east-1.amazonaws.com/awscodebuild-demo

### Configure AWS CLI

aws configure

aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin [IMAGEID].dkr.ecr.us-east-1.amazonaws.com

docker build -t awscodebuild-demo .

docker tag awscodebuild-demo:latest [IMAGEID].dkr.ecr.us-east-1.amazonaws.com/awscodebuild-demo:latest

docker push [IMAGEID].dkr.ecr.us-east-1.amazonaws.com/awscodebuild-demo:latest

Verify that docker image is listed under this ECR instance

## Configure GitHub Secrets

Under

Github.com > Settings > Secrets and variables > Actions

Set following secrets:

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

ECR_ADDRESS
