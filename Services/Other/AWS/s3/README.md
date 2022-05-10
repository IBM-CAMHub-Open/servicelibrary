# Amazon S3 Bucket

## Overview

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration uses the [AWS provider](https://www.terraform.io/docs/providers/aws/index.html) to provision a S3 bucket on AWS. 

This service is composed of following terraform templates:

[Amazon S3 Storage](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.5/AWS/terraform/hcl/storage)

You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

## Test Deploy the Service

To deploy this service from IBM Cloud Automation Manager navigate to Automate Infrastructure > Manage Services > Cloud Services > Virtual Machine on Amazon Web Services. Fill the following input parameters and deploy the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | AWS Connection             | |
| Region                          | string          | AWS Region                 | |
| S3 Bucket Name                  | string          | The name of the bucket to put the files in.                 | |
| ACL                             | string          | The canned ACL to apply. Defaults to private.                 | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | AWS Connection             | |
| Region                          | string          | AWS Region                 | |
| S3 Bucket Name                  | string          | The name of the bucket to put the files in.                 | |
| ACL                             | string          | The canned ACL to apply. Defaults to private.                 | |

### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0 