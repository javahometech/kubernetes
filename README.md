# Kubernetes
## Table of Contents
## Installing Kubernetes on AWS Using Kops
### One Linux/Ubuntu Virtual Machine is Required (Our Example is Based on AWS Linux)

```
Create a new IAM role for EC2 with admin access.
```

```
Attache IAM role to EC2 instance
```
### Install kops by following its [official installation guide](https://github.com/kubernetes/kops#linux).
```sh
$curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
$chmod +x kops-linux-amd64
$sudo mv kops-linux-amd64 /usr/local/bin/kops
```
##### Checking kops version.
```sh
$kops version
```
### Install kubectl by following its [official installation guide](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)
```sh
$curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
$curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.12.0/bin/linux/amd64/kubectl
$chmod +x ./kubectl
$sudo mv ./kubectl /usr/local/bin/kubectl
```
##### Checking kubectl version.
```sh
$kubectl version
```
### Create an AWS S3 bucket for kops to persist its state.
```sh
$bucket_name=sample-kops-state-store
$aws s3 mb s3://${bucket_name} --region us-west-2
```
### Create domain from free websites dot.tk

```
  Create Hosted Zone under AWS Route 53, Hosted Zone name must match with domain you created in previous step
```

```
  Takse DNS servers and update them in dot.tk under your domain name servers
```

### Provide a name for the Kubernetes cluster and set the S3 bucket URL in the following environment variables.
```sh
export KOPS_CLUSTER_NAME=sample.com
export KOPS_STATE_STORE=s3://${bucket_name}
```
### Create a ssh key pair before run the create cluster command this is used in 
```sh
$ssh-keygen
```
### kops create cluster help command to find additional parameters.
```sh
$kops create cluster --help
```
### Create a Kubernetes cluster definition using kops by providing the required fields.
```sh
$kops create cluster \
--state=${KOPS_STATE_STORE} \
--node-count=2 \
--master-size=t2.micro \
--node-size=t2.micro \
--zones=us-west-1a \
--name=${KOPS_CLUSTER_NAME}
```
### If it show any ssh required after running above command
```sh
$kops create secret sshpublickey admin -i ~/.ssh/id_rsa.pub --name=${KOPS_CLUSTER_NAME} --state=${KOPS_STATE_STORE}
```
### Review the Kubernetes cluster definition by executing the below command
```sh
$kops edit cluster --name=${KOPS_CLUSTER_NAME} --state=${KOPS_STATE_STORE}
```
### Now create the Kubernetes cluster on AWS by executing kops update command
```sh
$kops update cluster --name=${KOPS_CLUSTER_NAME} --state=${KOPS_STATE_STORE} --yes
```
### Above command may take some time to create the required infrastructure resources on AWS. Execute the validate command to check its status and wait until the cluster becomes ready
```sh
$kops validate cluster --state=${KOPS_STATE_STORE} --name=${KOPS_CLUSTER_NAME}
```
### Execute the below command to find the Kubernetes master hostname using kubectl
```sh
$kubectl cluster-info
```
### To connect to the master and check the connection
```sh
$ssh -i ~/.ssh/id_rsa admin@api.sample.com
```
### Destroy the kubernetes cluster using below command
```sh
$kops delete cluster --state=${KOPS_STATE_STORE} --name=${KOPS_CLUSTER_NAME} --yes
```
This site was built using [GitHub Pages](https://pages.github.com/).
