# Kubernetes
## Table of Contente
### Installing Kubernetes on AWS Using Kops
### Linux
#### 1st Insatll awscli using following 
```sh
$pip install awscli
```
#### Create a new IAM user or use an existing IAM user and grant following permissions.
- AmazonEC2FullAccess
- AmazonRoute53FullAccess
- AmazonS3FullAccess
- AmazonVPCFullAccess
#### Configure the AWS CLI by providing the Access Key, Secret Access Key and the AWS region.
```sh
$aws configure
```
```
AWS Access Key ID [None]: AccessKeyValue
AWS Secret Access Key [None]: SecretAccessKeyValue
Default region name [None]: us-east-1
Default output format [None]:
```
#### Install kops by following its [official installation guide](https://github.com/kubernetes/kops#linux).
```sh
$curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
$chmod +x kops-linux-amd64
$sudo mv kops-linux-amd64 /usr/local/bin/kops
```
##### Checking kops version.
```sh
$kops version
```
#### Create an AWS S3 bucket for kops to persist its state.
```sh
$bucket_name=sample-kops-state-store
$aws s3 mb s3://${bucket_name} --region us-west-2
```
#### Provide a name for the Kubernetes cluster and set the S3 bucket URL in the following environment variables.
```sh
export KOPS_CLUSTER_NAME=sample.com
export KOPS_STATE_STORE=s3://${bucket_name}
```
####
This site was built using [GitHub Pages](https://pages.github.com/).
