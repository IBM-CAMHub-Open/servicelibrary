# Single Virtual Machine on IBM Cloud

## Overview
![alt text](./VMOnIBMCloud.png)

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration uses the [IBM Cloud provider](https://cloud.ibm.com/docs/terraform?topic=terraform-tf-provider) to provision a Virtual Machine on IBM Cloud.

This service is composed of following terraform template

- [Virtual Server with SSH key](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.5/BlueMix/terraform/hcl/scenario1 ) terraform template.

You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. 
By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

* [Test Deploy the Service](#test-deploy-the-service)
* [Deploying the service from Service Library](#deploying-the-service-from-service-library)

## Test Deploy the Service

To deploy this service from IBM Cloud Automation Manager navigate to Automate Infrastructure > Manage Services  > Virtual Machine > Virtual Machine on IBM Cloud. Fill the following input parameters and deploy the service.

| Parameter name                  | Type            | Parameter description             | Allowed values |
| :---                            | :---            | :---                              | :---           |
| Connection                      | connection      | IBM Cloud Connection              | |
| public_ssh_key                  | string          | Public SSH key used to connect to the virtual guest                                                                                   | |
| hostname                        | string          | Hostname of the virtual instance (small flavor) to be deployed                                                                          | |
| domain                          | string          | Domain of the virtual instance to be deployed                                                                                | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

| Parameter name                  | Type            | Parameter description             | Allowed values |
| :---                            | :---            | :---                              | :---           |
| Connection                      | connection      | IBM Cloud Connection              | |
| public_ssh_key                  | string          | Public SSH key used to connect to the virtual guest                                                                                   | |
| hostname                        | string          | Hostname of the virtual instance (small flavor) to be deployed                                                                          | |
| domain                          | string          | Domain of the virtual instance to be deployed                                                                                | |


### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0  
 