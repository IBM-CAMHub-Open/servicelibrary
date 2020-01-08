# OpenShift Container Platform 4.2 cluster on VMware 

## Overview
This service deploys OpenShift Container Platform (OCP) cluster version 4.2 on Amazone EC2 and import it into an existing IBM Multi Cloud Manager (MCM) controller.

The first activity of the service is to deploy a new [OpenShift Container Platform Enterprise Installation](https://github.com/IBM-CAMHub-Open/template_openshift_installer/tree/4.2/vmware/terraform). Refer to the template documentation for more details. 

The second activity of the service is [Import OpenShift Container Platform Kubernetes cluster into MCM hub-cluster](https://github.com/IBM-CAMHub-Open/template_mcm_install/tree/3.2.1/OCP/terraform) It performs a MCM import which will register the newly deployed OCP cluster with an existing MCM controller(hub) 

## Service input Paramters

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| Cloud Connection | | Name of the AWS connection used to deploy the OpenShift Container Platform |
| MCM Controller | | Name of the MCM Controller to import the OCP cluster into. |
| Region | us-east-2 | AWS region to deploy your ICP cluster nodes. The AWS selected region should have at least 3 availability zones. |
| Availability Zones | [a, b, c] | The availability zone letter identifier in the above selected region. The AWS selected region should have at least 3 availability zones. |
| Key Pair Name |  | Name of the EC2 key pair. |
| Key Pair Private Key |  | Base64 encoded private key file contents of the EC2 key pair. |
| S3 Bucket |  | The s3 bucket name that will store the ignition files required for OPENSHIFT cluster nodes.
| Redhat Pull Secret | | Base64 encoded Redhat Pull Secret. Used to pull Openshift related install files.
| Cluster Name | openshift-cluster | OPENSHIFT cluster prefix. Used to prefix a randon string used to name and tag VPC and other AWS resources created for OPENSHIFT nodes. | 
| Public Domain Name |  | The domain entered must be in the Route53 public hosted zone. |
| VPC CIDR | 10.0.0.0/16 | The CIDR block for the VPC | 
| Public Subnet CIDRs | [10.0.10.0/24, 10.0.11.0/24, 10.0.12.0/24], | Used for the bastion, bootstrap nodes and the public facing load balancers. You must provide one for each availability zone. | 
| Private Subnet CIDRs | [ 10.0.20.0/24, 10.0.21.0/24, 10.0.22.0/24], | Used for the OpenShift cluster nodes, and private load balancers. You must provide one for each availability zone. | 
| Instance Type | t2.micro | List of Recommended Instance types. | 
| Disk Size (GiB) | 50 | Enter size of root disk in gibibytes | 
| Instance Type | t2.micro | List of Recommended Instance types. | 
| Disk Size (GiB) | 50 | Enter size of root disk in gibibytes | Create or destroy bootstrap for the OpenShift install.  Required for installation.  Should be removed after successful installion. | 
| Number of Master Nodes | 3 | Enter a valid number of master nodes - between 3 and 100.
| Instance Type | m4.xlarge | List of Recommended Instance types. | 
| Disk Size (GiB) | 120 | Enter size of root disk in gibibytes. | 
| Number of Worker Nodes | 3 | Enter a valid number of master nodes - between 2 and 100.
| Instance Type | m4.large | List of Recommended Instance types. | 
| Disk Size (GiB) | 120 | Enter size of root disk in gibibytes. | 

### License and Maintainer

Copyright IBM Corp. 2019

Service Version - 4.2.0  