# Kops

## Kops Installation
* sudo wget https://github.com/kubernetes/kops/releases/download/1.13.2/kops-linux-amd64
* sudo chmod +x kops-linux-amd64 
* sudo mv kops-linux-amd64 /usr/local/bin/kops
* kops version

## Configure aws
On AWS IAM create user called "kops" with programmatic access. 
Give required privileges:
Administrator access

In the real production environment give the following privileges:
* AmazonEC2FullAccess
* AmazonRoute53FullAccess
* AmazonS3FullAccess
* IAMFullAccess
* AmazonVPCFullAccess

run the command:
* aws configure
AWS Access Key ID [None]: Access key here
AWS Secret Access Key [None]: Secret key here
Default region name [None]: us-east-1 (give any region you are creating you cluster)
Default output format [None]: text

## Route53 configure
Create Hosted zone
Create Record set with you domain name: 
* Record set name = kops.mr.robot.com
* Type = NS - Name Server
* Value = the same value in the domain name server

## Create S3 Bucket
Create private bucket on aws S3 : kops.mr.robot.com

## Install kubectl
* curl -o kubectl https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/darwin/amd64/kubectl
* chmod +x ./kubectl
* mv kubectl /usr/bin/

## Create Cluster
Run the following commands:
* export KOPS_STATE_STORE=s3://kops.mr.robot.com
* export NAME=kops.mr.robot.com
* ssh-keygen (enter 4 times)
* kops create secret --name kops.mr.robot.com sshpublickey admin -i ~/.ssh/id_rsa.pub
* kops create cluster --node-count 3 --master-count=3 --zones us-east-1a,us-east-1b,us-east-1c  --master-zones us-east-1a,us-east-1b,us-east-1c  --dns-zone ${NAME} --node-size t2.medium  --master-size t2.medium --topology public --networking weave --cloud-labels "Team=dev,Owner=Murodbey" ${NAME} --yes


## Cluster deletion
kops delete cluster kops.mr.robot.com --yes