# Single Virtual Machine on Amazon Web Services

## Overview
![alt text](./VMOnAWS.png)

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration uses the [AWS provider](https://www.terraform.io/docs/providers/aws/index.html) to provision a Virtual Machine on AWS.

This service is composed of following terraform template

- [Amazon EC2 Virtual Server with SSH key](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.4/AWS/terraform/singlefile/hcl) terraform template.

You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. 
By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

* [Test Deploy the Service](#test-deploy-the-service)
* [Deploying the service from Service Library](#deploying-the-service-from-service-library)

## Test Deploy the Service

To deploy this service from IBM Cloud Automation Manager navigate to Automate Infrastructure > Manage Services > Virtual Machine > Virtual Machine on Amazon Web Services. Fill the following input parameters and deploy the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | AWS Connection             | |
| region                          | string          | AWS Region                 | |
| vpc_name_tag                    | string          | Name of the Virtual Private Cloud (VPC) this resource is going to be deployed into                                            | |
| subnet_name                     | string          | Subnet Name                | |
| public_ssh_key_name             | string          | Name of the public SSH key used to connect to the virtual guest                                                                | |
| public_ssh_key                  | string          | Public SSH key used to connect to the virtual guest                                                                            | |
| aws_image                       | string          | Operating system image id / template that should be used when creating the virtual image                                   | |
| aws_image_size                  | string          | AWS Image Instance Size    | |
| aws_ami_owner_id                | string          | AWS AMI Owner ID           | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | AWS Connection             | |
| region                          | string          | AWS Region                 | |
| vpc_name_tag                    | string          | Name of the Virtual Private Cloud (VPC) this resource is going to be deployed into                                            | |
| subnet_name                     | string          | Subnet Name                | |
| public_ssh_key_name             | string          | Name of the public SSH key used to connect to the virtual guest                                                                | |
| public_ssh_key                  | string          | Public SSH key used to connect to the virtual guest                                                                            | |
| aws_image                       | string          | Operating system image id / template that should be used when creating the virtual image                                   | |
| aws_image_size                  | string          | AWS Image Instance Size    | |
| aws_ami_owner_id                | string          | AWS AMI Owner ID           | |

### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0 
 