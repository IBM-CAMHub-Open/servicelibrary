# Single Virtual Machine on Microsoft Azure

## Overview
![alt text](./VMOnAzure.png)

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/en/SS2L37/product_welcome_cloud_automation_manager.html) service configuration uses the [Microsoft Azure provider](https://www.terraform.io/docs/providers/azure/index.html) to provision a Virtual Machine on Microsoft Azure.

More details on IBM Cloud Automation Manager Service can be found [here](https://www.ibm.com/support/knowledgecenter/en/SS2L37_4.2.0.0/cam_managing_services.html).

This service is composed of following terraform template

- [Virtual Machine with SSH key on Microsoft Azure](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.4/Azure/terraform/hcl/singlevirtualmachine) terraform template.

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > Virtual Machine > Virtual Machine on Microsoft Azure. Fill the following input parameters and deploy the service.

Note: The parameters indicated as _(hidden)_ have default values.  If you need to change them, make a copy of this service configuration and create a new service in IBM Cloud Automation Manager with the new configuration. 

| Parameter name                  | Type            | Parameter description                    | Allowed values |
| :---                            | :---            | :---                                     | :---           |
| Connection                      | connection      | Microsoft Azure Connection               | |
| azure_region                    | string          | Azure region to deploy infrastructure resources                                                                                      | |
| name_prefix                     | string          | Prefix of names for Azure resources                                                                                      | |
| admin_user                      | string          | Name of an administrative user to be created in virtual machine in this deployment                                                             | |
| admin_user_password             | password        | Password of the newly created administrative usert                                                                                          | |
| user_public_key                 | string          | Public SSH key used to connect to the virtual machine                                                                                        | |

Service offers two plans standard and advance. The standard plan offers quick deployment through a few pre-configured parameters, Hence you only need to provide values of remaining parameters. The advance plan gives you full control over configuration. In the advance plan, you are required to provide values of all the parameters.

### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0 
 