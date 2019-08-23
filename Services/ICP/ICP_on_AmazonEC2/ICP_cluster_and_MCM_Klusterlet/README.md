# Highly Available ICP Deployment with klusterlet on Amazon EC2

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/en/SS2L37/product_welcome_cloud_automation_manager.html) service configuration first uses the [AWS provider](https://www.terraform.io/docs/providers/aws/index.html) to provision virtual machines on AWS to prepare VMs and deploy [IBM Cloud Private](https://www.ibm.com/cloud-computing/products/ibm-cloud-private/) 3.2.0 on them.  This configuration then installs the necessary [IBM Multicloud Manager](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.2.0/mcm/getting_started/introduction.html) 3.2.0 assets to the deployed ICP and deploys the [IBM MCM klusterlet provider](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.2.0/mcm/installing/klusterlet.html) (ibm-mcmk-prod helm chart) 3.2.0 to make this ICP deployment a managed cluster. More details on IBM Cloud Automation Manager Service can be found [here](https://www.ibm.com/support/knowledgecenter/en/SS2L37_3.2.1.0/cam_managing_services.html).

This service is composed of following terraform templates

- [IBM Cloud Private 3.2.0 highly-available cluster in AWS](https://github.com/IBM-CAMHub-Open/template_icp_aws) terraform template.
- [IBM Multicloud Manager 3.2.0](https://github.com/IBM-CAMHub-Open/template_mcm_install/tree/3.2.0/ICP/terraform) terraform template and 


This service can be either deployed from IBM Cloud Automation Manager or from IBM Cloud Private Catalog.

* [Deploying the service from IBM Cloud Automation Manager](#deploying-the-service-from-ibm-cloud-automation-manager)
* [Deploying the service from IBM Cloud Private Catalog](#deploying-the-service-from-ibm-cloud-private-catalog)

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > ICP on Amazon EC2 > ICP cluster with klusterlet on Amazon EC2. Fill the following input parameters and deploy the service.

Note: Bastion Node, Master Node, Proxy Node, Management Node, Worker Node and Vulnerability Advisor Node are hidden parameters. If you need to change them then make a copy of this service configuration and create a new sevice in IBM Cloud Automation Manager with the new configuration. 

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| AWS Region | us-east-1 | AWS region to deploy your ICP cluster nodes. For an HA installation, the AWS selected region should have at least 3 availability zones. |
| Availability Zones | ["a","b","c"] | The availability zone letter identifier in the above selected region. For high availability should have at least 3 availability zones. Setting to a single availability zone will disable high availability and not provision EFS, in this case, reduce the number of master and proxy nodes to 1. If you are installing this service from ICP Catalog, your input should look like ["a", "b"]" |
| Key Name |  | Name of the EC2 key pair. |
| Private Key |  | Base64 encoded private key file contents of the EC2 key pair. |
| VPC Name | icp-vpc | AWS VPC Name prefix. This value is used to prefix the VPC created for ICP nodes. |
| Amazon Machine Image (AMI-ID) | ami-0f9cf087c1f27d9b1 | Default Amazon Machine Image ID that will be used if AMI ID for individual node is not provided. |
| Bastion Node | {"nodes":"1","type":"t2.micro","ami":"ami-0f9cf087c1f27d9b1","disk":"10"} | Bastion host that you can use to ssh into ICP cluster nodes. Can be used for debugging purpose. |
| Master Node | {"nodes":"3","type":"m4.2xlarge","ami":"ami-0f9cf087c1f27d9b1","disk":"300","docker_vol":"100","ebs_optimized":true} | Master node details. Each master node will be created in a different AZS. Number of AZS, public subnet and private subnet must match the number of master node. |
| Proxy Node | {"nodes":"3","type":"m4.xlarge","ami":"ami-0f9cf087c1f27d9b1","disk":"150","docker_vol":"100","ebs_optimized":true} | Proxy node details. Each proxy node will be created in a different AZS. Number of AZS, public subnet and private subnet must match the number of proxy node. |
| Management Node | {"nodes":"3","type":"m4.2xlarge","ami":"ami-0f9cf087c1f27d9b1","disk":"300","docker_vol":"100","ebs_optimized":true} | Management node details. Each management node will be created in a different AZS. Number of AZS, public subnet and private subnet must match the number of management node. |
| Worker Node | {"nodes":"3","type":"m4.2xlarge","ami":"ami-0f9cf087c1f27d9b1","disk":"150","docker_vol":"100","ebs_optimized":true} | Worker node details. Each worker node will be created in a different AZS. Number of AZS, public subnet and private subnet must match the number of worker node. |
| Vulnerability Advisor Node | {"nodes":"3","type":"m4.2xlarge","ami":"ami-0f9cf087c1f27d9b1","disk":"300","docker_vol":"100","ebs_optimized":true} | Vulnerability Advisor node details. Each VA node will be created in a different AZS. Number of AZS, public subnet and private subnet must match the number of VA node. |
| Cluster Name | icp | ICP Cluster Name |
| ICP Password |  | ICP user password |
| Docker Package Location |  | Docker package location is required when installing ICP EE on RedHat. Package is expected in AWS s3 bucket. Prefix the location string with protocol s3://.  |
| ICP EE Image Location |  | Image location of ICP EE. Package is expected in AWS s3 bucket. Prefix the location string with s3://. |
| ICP Inception Image | ibmcom/icp-inception-amd64:3.2.0-ee | Name of the bootstrap installation image. |
| VPC CIDR block | 10.10.0.0/16 | AWS VPC CIDR block. This is the primary CIDR block for your ICP node VPC. |
| Subnet Name | icp-subnet | Subnet name prefix for public and private subnets used by ICP nodes. |
| Private Subnet CIDRs | ["10.10.10.0/24","10.10.11.0/24","10.10.12.0/24"] | List of subnet CIDRs. Total number of CIDR entry must match the number of availability zone provided above. A CIDR value is used in the creation of a private subnet in an availability zone for the worker nodes. |
| Public Subnet CIDRs | ["10.10.20.0/24","10.10.21.0/24","10.10.22.0/24"] | List of subnet CIDRs. Total number of CIDR entry must match the number of availability zone provided above. A CIDR value is used in the creation of a public subnet in an availability zone for the proxy and management nodes. |
| Private Domain | icp-cluster.icp | Private domain name that is used to create route53 name. |

## Deploying the service from IBM Cloud Private Catalog

To deploy this service from IBM Cloud Private Catalog navifate to Catalog, search the Catalog for icp-cluster-with-klusterlet-on-amazon-ec2 and fill the following input parameters and install the service.

Note: Bastion Node, Master Node, Proxy Node, Management Node, Worker Node and Vulnerability Advisor Node are hidden parameters. If you need to change them then make a copy of this service configuration, create a new sevice in IBM Cloud Automation Manager with the new configuration and publish the service to ICP catalog.

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| aws_region | | AWS region to deploy your ICP cluster nodes. For an HA installation, the AWS selected region should have at least 3 availability zones. |
| aws_azs | | The availability zone letter identifier in the above selected region. For high availability should have at least 3 availability zones. Setting to a single availability zone will disable high availability and not provision EFS, in this case, reduce the number of master and proxy nodes to 1. If you are installing this service from ICP Catalog, your input should look like ["a", "b"]. |
| aws_key_name |  | Name of the EC2 key pair. |
| aws_privatekey |  | Base64 encoded private key file contents of the EC2 key pair. |
| aws_vpcname | icp-vpc | AWS VPC Name prefix. This value is used to prefix the VPC created for ICP nodes. |
| aws_ami | ami-0f9cf087c1f27d9b1 | Default Amazon Machine Image ID that will be used if AMI ID for individual node is not provided. |
| icp_instance_name | icp | ICP Cluster Name |
| icp_password |  | ICP user password |
| icp_docker_package_location |  | Docker package location is required when installing ICP EE on RedHat. Package is expected in AWS s3 bucket. Prefix the location string with protocol s3://.  |
| icp_image_location |  | Image location of ICP EE. Package is expected in AWS s3 bucket. Prefix the location string with s3://. |
| icp_inception_image | ibmcom/icp-inception-amd64:3.2.0-ee | Name of the bootstrap installation image. |
| aws_cidr | 10.10.0.0/16 | AWS VPC CIDR block. This is the primary CIDR block for your ICP node VPC. |
| aws_subnetname | icp-subnet | Subnet name prefix for public and private subnets used by ICP nodes. |
| aws_subnet_cidrs | | List of subnet CIDRs. Total number of CIDR entry must match the number of availability zone provided above. A CIDR value is used in the creation of a private subnet in an availability zone for the worker nodes. If you are installing this service from ICP Catalog, your input should look like ["10.10.10.0/24", "10.10.11.0/24"].|
| aws_pub_subnet_cidrs | | List of subnet CIDRs. Total number of CIDR entry must match the number of availability zone provided above. A CIDR value is used in the creation of a public subnet in an availability zone for the proxy and management nodes. If you are installing this service from ICP Catalog, your input should look like ["10.10.20.0/24", "10.10.21.0/24"].|
| Paws_private_domain | icp-cluster.icp | Private domain name that is used to create route53 name. |

### License and Maintainer

Copyright IBM Corp. 2019

Service Version - 3.2.0  
 