# OpenShift Container Platform Cluster on Amazon EC2 with RHACM import 

## Overview
This service deploys OpenShift Container Platform (OCP) cluster version 4.2 on Amazone EC2 and imports it into an Red Hat Advanced Cluster Management enabled IBM CLoud Pak for Multi Cloud Manager 2.x.

The first activity of the service is to deploy a new [OpenShift Container Platform Enterprise Installation](https://github.com/IBM-CAMHub-Open/template_openshift_installer/tree/4.2/terraform12/aws/terraform). Refer to the template documentation for more details. 

The second activity of the service is [Import OpenShift Container Platform Kubernetes cluster into RHACM enabled IBM CP4MCM](https://github.com/IBM-CAMHub-Open/template_import_rhacm/tree/5.1.0/terraform12/OCP/terraform) that imports the OCP kubernetes cluster into Red Hat Advanced Cluster Management enabled IBM CLoud Pak for Multi Cloud Manager 2.x. 

## Service input Paramters

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| Cloud Connection | | Name of the AWS connection used to deploy the OpenShift Container Platform |
| OpenShift Container Platform Login Information     |  | This shared parameter contains details of the OCP on which RHACM enabled IBM CP4MMCM is installed. This newly created cluster will be registered to this RHACM and IBM CP4MCM. Pointing to a data object created from the [oc_login_info](https://github.com/IBM-CAMHub-Open/template_import_rhacm/blob/5.1.0/terraform12/datatypes/ocp.json) data type| |
| Region | us-east-2 | AWS region to deploy your ICP cluster nodes. The AWS selected region should have at least 3 availability zones. |
| Availability Zones | [a, b, c] | The availability zone letter identifier in the above selected region. The AWS selected region should have at least 3 availability zones. |
| Key Pair Name |  | Name of the EC2 key pair. |
| Key Pair Private Key |  | Base64 encoded private key file contents of the EC2 key pair. |
| S3 Bucket |  | The s3 bucket name that will store the ignition files required for OPENSHIFT cluster nodes.
| Redhat Pull Secret | | Base64 encoded Redhat Pull Secret. Used to pull Openshift related install files.
| Cluster Name | oc-cluster | OPENSHIFT cluster prefix. Used to prefix a randon string used to name and tag VPC and other AWS resources created for OPENSHIFT nodes. Cluster name can have lower case alphabets, numbers and dash. Must start with lower case alphabet and end with alpha-numeric character. Maximum length is 10 characters. | 
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

Copyright IBM Corp. 2020

Service Version - 4.2.0.1