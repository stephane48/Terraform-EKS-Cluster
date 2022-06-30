# Terraform - Creating an EKS Cluster with Worker Node Group

## DEVELOPMENT
### STEP 01 - Provide Networking part
I'm using my own terraform module to create the vpc, subnets, internet gateway, nat gateways etc

### STEP 03 - IAM ROLES
#### EKS Cluster Role
Kubernetes clusters managed by Amazon EKS make calls to other AWS services on your behalf to manage the resources that you use with the service. That's why I create this role
#### NODE GROUP ROLE
The Amazon EKS node kubelet daemon makes calls to AWS APIs on your behalf. Nodes receive permissions for these API calls through an IAM instance profile and associated policies. Before you can launch nodes and register them into a cluster, you must create an IAM role for those nodes to use when they are launched.
#### ATTACH MANAGED IAM POLICIES TO IAM ROLES
This policy provides Kubernetes the permissions it requires to manage resources on your behalf. Kubernetes requires Ec2:CreateTags permissions to place identifying information on EC2 resources including but not limited to Instances, Security Groups, and Elastic Network Interfaces.
### STEP 04 - Create EKS Cluster
Must set up the arn of the IAM cluster role, kubernetes version and vpc configuration
#### NODE GROUP
To create and run PODS we need a infrastructure. We can select between EC2 instances (worker nodes) or FARGATE.
For this implementation I'm gonna provide EC2 "t3-micro" instances as worker nodes to run the PODS
For an isolated infrastructure and more security, the best practice is to create your worker nodes in private subnets.
We must provide the required information about the AMI, intance type, capacity type, disk size to create the worker nodes and also scaling configuration to specify the desired, max and min size of worker nodes
### STEP 05 - Check Cluster & Node Group Creation
Check if the node gruoup was created using AWS Console

Create or update the kubeconfig for Amazon EKS
For this purpose use this command:

```aws eks update-kubeconfig --region <region-code> --name <cluster-name>```

Replace ```<region-code>``` with you respective region, example ```us-east-1```
and ```<cluster-name>``` with your cluster's name


## Architecture
![EKSclsuter](img/architecture.png)

```C++
Copyright © 2022 All Rights Reserved by Stephane Kamdem Kamguia.
