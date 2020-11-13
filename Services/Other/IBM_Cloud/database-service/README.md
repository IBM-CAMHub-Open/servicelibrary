# IBM Database Service

## Overview

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration uses the IBM terraform provider to provision a Database Service IBM Cloud.

This service is composed of following terraform templates:

[IBM Database Service](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.4/IBM_Cloud/database-service) terraform template which creates a DB instance of the IBM Database Service . 

You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

## Test Deploy the Service

To deploy this service from IBM Cloud Automation Manager navigate to Automate Infrastructure > Manage Services > Cloud Services > Virtual Machine on Amazon Web Services. Fill the following input parameters and deploy the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | IBM Connection             | |
| Resource Group                  | string      	| IBM Cloud resource groups  | |
| Region                          | string          | IBM Region                 | |
| Database Service				  | string          | IBM Database Service to use 	| |
| Serivce Plan                    | string          | Plan for the Database Service | |
| Serivce version                 | string          | The version of the database to be provisioned. If omitted, the database is created with the most recent major and minor version. | |
| DB Instance Name                | string          | The name of the database instance to be created. | Must begin with a letter and contain only alphanumeric characters.|
| DB Password                     | string          | Password for the DB admin user. | At least 32 ASCII characters and maximum of 32 characters. Can't contain any of the following: forward slash, single quote, double quote and @.|              | |
| Memory allocation                    | string          | The amount of memory in megabytes for the database, split across all members. | |
| Disk allocation                    | string          | The amount of disk space for the database, split across all members. | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | IBM Connection             | |
| Resource Group                  | string      	| IBM Cloud resource groups  | |
| Region                          | string          | IBM Region                 | |
| Database Service				  | string          | IBM Database Service to use 	| |
| Serivce Plan                    | string          | Plan for the Database Service | |
| Serivce version                 | string          | The version of the database to be provisioned. If omitted, the database is created with the most recent major and minor version. | |
| DB Instance Name                | string          | The name of the database instance to be created. | Must begin with a letter and contain only alphanumeric characters.|
| DB Password                     | string          | Password for the DB admin user. | At least 32 ASCII characters and maximum of 32 characters. Can't contain any of the following: forward slash, single quote, double quote and @.|              | |
| Memory allocation                    | string          | The amount of memory in megabytes for the database, split across all members. | |
| Disk allocation                    | string          | The amount of disk space for the database, split across all members. | |

### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0 
