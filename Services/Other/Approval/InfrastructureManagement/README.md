# Infrastructure Management Approval

## Overview
![alt text](./Infrastructure_Management_Approval.png)

This [Managed services](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service is used to get approval from Infrastructure Management before provisioning the resources.

More details on Managed services Service can be found [here](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html).

This service is composed of following terraform template

- [Poll Infrastructure Management for Approval](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.4/Other/Approval/InfrastructureManagement) terraform template.

## Deploying the service from Managed services

### Prerequisites

- Navigate to `Manage` -> `Shared parameters` -> `Create data type` -> Enter Name as `Infrastructure Management Authentication Details`, Data type as `im_auth` and Description as `Authentication details such as username and password to connect to Infrastructure Management` -> `Create` -> `Add Attributes`. Fill the following attributes:

| Parameter name                  | End-user permission   | Parameter type             | Display name   |
| :---                            | :---                  | :---                       | :---           |
| username                        | true                  | string                     | Username       |
| password                        | true                  | password                   | Password       |

- Navigate to `Manage` -> `Shared parameters` -> In `Search data types`, Enter "Infrastructure Management Authentication Details" -> Verify Data type is present
- Go to `Create data object` -> Select data type "im_auth" -> Enter Data Object Name for e.g. "im_auth". Fill the following paramaters.

| Parameter name                  | Type            | Parameter description
| :---                            | :---            | :---
| Username                        | string          | Username to connect to  Infrastructure Management
| Password                        | password        | Password to connect to Infrastructure Management

- Navigate to `Library` -> `Services` ->  `Approval` -> `Infrastructure Management Approval` -> Navigate to `1.0.0.0` version -> Edit -> Composition -> Click on `Resthook` -> Go to `Create` section -> Enter Infrastructure Management username in `Auth username` and Infrastructure Management password in `Auth password` -> `Save` 

To deploy this service from Managed services navigate to `Library` -> `Services` ->  `Approval` -> `Infrastructure Management Approval`. Fill the following input parameters and deploy the service.

Note: The parameters indicated as _(hidden)_ have default values.  If you need to change them, make a copy of this service configuration and create a new service in Managed services with the new configuration.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Admin Email                    | string          | Email where approval status to be send                                            | |
| Infrastructure Management Authentication Details                          | Shared Parameter          | Shared Parameter to connect to Infrastructure Management                 | im_auth|
| CURL Option                     | string          | Options for curl command used to retrieve status from Infrastructure Management e.g. --insecure                | |
| Wait Time              | string          | Wait time in seconds i.e. time after which poll should again happen to retrieve the approval status 
| URL                    | string          | Infrastructure Management URL to submit approval request                                            | |
| Payload                    | string          | Payload to submit approval request                                            | |

Service offers one standard plan. The standard plan offers quick deployment through a few pre-configured parameters, Hence you only need to provide values of remaining parameters.

### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0
 