# Amazon Relational Database Service

## Overview

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration uses the [AWS provider](https://www.terraform.io/docs/providers/aws/index.html) to provision a Relational Database Service (RDS) on AWS. Using this service the RDS instance can either be provisioned from an existing snapshot or create a new RDS from scratch. 

This service also provides custom action on deployed service instance to create a snapshot of the provisioned database instance.

This service is composed of following terraform templates:

[Amazon Relational Database Service](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.5/AWS/terraform/hcl/rds) terraform template which creates a RDS instance from an existing snapshot or create a new RDS from scratch. 

[Amazon Relational Database Service Snapshot](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.5/AWS/terraform/hcl/rds) terraform template which is used in managed service custom action to create a snapshot of provisioned database instance.

You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

## Test Deploy the Service

To deploy this service from IBM Cloud Automation Manager navigate to Automate Infrastructure > Manage Services > Cloud Services > Virtual Machine on Amazon Web Services. Fill the following input parameters and deploy the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | AWS Connection             | |
| Region                          | string          | AWS Region                 | |
| Snapshot Identifier             | string          | Snapshot ID to create the new database from. You must either provide this value or to create a fresh database provide values for Allocated Storage,  Database engine, Master DB user name and Master DB user password                 | |
| DB Engine                       | string          | The database engine to use to create a new RDS instance. Required unless a snapshot identifier is provided. If provided with snaphsot identifier, then this value must match the snapshot engine name.                 | |
| Allocated Storage               | string          |The allocated storage in gibibytes. Required unless a snapshot identifier is provided.                 | |
| DB Username                     | string          | User name for the master DB. Required unless a snapshot identifier is provided.                | Must begin with a letter and contain only alphanumeric characters. Maximum length is 16 characters.|
| DB Password                     | string          | Password for the master DB user. Required unless a snapshot identifier is provided.                 | At least 8 ASCII characters. Can't contain any of the following: forward slash, single quote, double quote and @.|
| DB Engine Version               | string          | The database engine version to use. If empty, it would pick the latest.                 | |
| Instance Class                  | string          |The instance type of the RDS instance.                 | |
| DB Instance Name                | string          | The name of the database to create when the DB instance is created. This value is also used as prefix for RDS instance unique identifier.                 | Must begin with a letter and contain only alphanumeric characters.|
| License Model                   | string          | License model information for this DB instance.                 | Must be one of the following values license-included, bring-your-own-license or general-public-license |
| Subnet Group Name                          | string          | DB instance will be created in the VPC associated with the DB subnet group. If unspecified, will be created in the default VPC, or in EC2 Classic, if available.                 | |
| VPC Security Group IDs                          | string          | List of VPC security groups to associate with RDS.                 | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| Connection                      | connection      | AWS Connection             | |
| Region                          | string          | AWS Region                 | |
| Snapshot Identifier             | string          | Snapshot ID to create the new database from. You must either provide this value or to create a fresh database provide values for Allocated Storage,  Database engine, Master DB user name and Master DB user password                 | |
| DB Engine                       | string          | The database engine to use to create a new RDS instance. Required unless a snapshot identifier is provided. If provided with snaphsot identifier, then this value must match the snapshot engine name.                 | |
| Allocated Storage               | string          |The allocated storage in gibibytes. Required unless a snapshot identifier is provided.                 | |
| DB Username                     | string          | User name for the master DB. Required unless a snapshot identifier is provided.                | Must begin with a letter and contain only alphanumeric characters. Maximum length is 16 characters.|
| DB Password                     | string          | Password for the master DB user. Required unless a snapshot identifier is provided.                 | At least 8 ASCII characters. Can't contain any of the following: forward slash, single quote, double quote and @.|
| DB Engine Version               | string          | The database engine version to use. If empty, it would pick the latest.                 | |
| Instance Class                  | string          |The instance type of the RDS instance.                 | |
| DB Instance Name                | string          | The name of the database to create when the DB instance is created. This value is also used as prefix for RDS instance unique identifier.                 | Must begin with a letter and contain only alphanumeric characters.|
| License Model                   | string          | License model information for this DB instance.                 | Must be one of the following values license-included, bring-your-own-license or general-public-license |
| Subnet Group Name                          | string          | DB instance will be created in the VPC associated with the DB subnet group. If unspecified, will be created in the default VPC, or in EC2 Classic, if available.                 | |
| VPC Security Group IDs                          | string          | List of VPC security groups to associate with RDS.                 | |

## Deploying custom action to create snapshot from service instance

To deploy the custom action to create snapshot from the service instance, on custom action you need provide the following parameter

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
|DB Snapshot Identifier           | string          | The Identifier for the snapshot.| Only alphanumeric characters and hyphens allowed. First character must be a letter. Cannot end with a hyphen or contain two consecutive hyphens.|

### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0 