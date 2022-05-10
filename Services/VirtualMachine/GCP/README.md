# Single Virtual Machine on Google Cloud Platform

## Overview
![alt text](./VMOnGCP.png)

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration uses the [Google Cloud Platform provider](https://www.terraform.io/docs/providers/google/index.html) to provision a Virtual Machine on Google Cloud Platform.

This service is composed of following terraform template

- [Google Cloud Single Virtual Machine Example](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.5/Google/terraform/hcl/singleVM) terraform template.

You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. 
By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

* [Test Deploy the Service](#test-deploy-the-service)
* [Deploying the service from Service Library](#deploying-the-service-from-service-library)

## Test Deploy the Service

To deploy this service from IBM Cloud Automation Manager navigate to Automate Infrastructure > Manage Services > Virtual Machine > Virtual Machine on Google Cloud Platform. Fill the following input parameters and deploy the service.

| Parameter name                  | Type            | Parameter description          | Allowed values |
| :---                            | :---            | :---                           | :---           |
| Connection                      | connection      | GCP Connection                 | |
| unique_resource_name            | string          | A unique name for the resource, required by GCE                                                                                  | |
| gce_ssh_public_key              | string          | Public SSH key to be injected into the authorized_keys of the guest VM                                                      | |
| gce_ssh_user                    | string          | User name to connect to the deployed VMs                                                                                  | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

| Parameter name                  | Type            | Parameter description          | Allowed values |
| :---                            | :---            | :---                           | :---           |
| Connection                      | connection      | GCP Connection                 | |
| unique_resource_name            | string          | A unique name for the resource, required by GCE                                                                                  | |
| gce_ssh_public_key              | string          | Public SSH key to be injected into the authorized_keys of the guest VM                                                      | |
| gce_ssh_user                    | string          | User name to connect to the deployed VMs                                                                                  | |

### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0  
 