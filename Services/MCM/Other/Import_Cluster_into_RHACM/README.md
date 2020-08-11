# Existing kubernetes cluster imported into Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management

## Overview
![alt text](./MCMonROKS.jpg)

This service imports an existing kubernetes cluster into the [Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) 2.x hub-cluster to make it a managed cluster.

More details on IBM Cloud Automation Manager Service can be found [here](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html).

This service is composed of following terraform templates

- [Import a kubernetes cluster into RHACM enabled IBM CP4MCM](https://github.com/IBM-CAMHub-Open/template_import_rhacm/tree/5.1.0/terraform12/other/mcm-klusterlet) terraform template.


This service can be either deployed from IBM Cloud Automation Manager or from IBM Cloud Pak for Multicloud Management.

* [Deploying the service from IBM Cloud Automation Manager](#deploying-the-service-from-ibm-cloud-automation-manager)
* [Deploying the service from IBM Cloud Pak for Multicloud Management Service Library](#deploying-the-service-from-ibm-cloud-private-catalog)

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > Import a kubernetes cluster into RHACM enabled IBM CP4MCM. Fill the following input parameters and deploy the service.


| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---        |
| cloud_connection                | cloudconnection | Name of the IBM cloud connection used to deploy the ROKS cluster. |
| cluster_name                    | string          | Name of the ROKS cluster. Cluster name can have lower case alphabets, numbers and dash. Must start with lower case alphabet and end with alpha-numeric character. Maximum length is 32 characters. |
| OpenShift Container Platform Login Information     | sharedparameter | Details of the OCP on which RHACM enabled IBM CP4MMCM is installed. This newly created cluster will be registered to this RHACM and IBM CP4MCM. Pointing to a data object created from the [oc_login_info](https://github.com/IBM-CAMHub-Open/template_import_rhacm/blob/5.1.0/terraform12/datatypes/ocp.json) data type| |
| cluster_endpoint                | string | URL for the target Kubernetes cluster endpoint |
| cluster_user                    | string | Username for accessing the target Kubernetes cluster |
| cluster_token                   | string | Token for authenticating with the target Kubernetes cluster |
| image_registry                  | URL for private docker registry from which klusterlet images will be pulled | |
| image_suffix                    | Suffix (e.g. -amd64), corresponding to the platform type, to be appended to image name | |
| image_version                   | Version/Tag (e.g 2.0.0 or latest) of the MCM image to be pulled | |
| docker_user                     | Username for authenticating with the private docker registry | |
| docker_password                 | Password for authenticating with the private docker registry | |

## Deploying the service from IBM Cloud Pak for Multicloud Management Service Library

To deploy this service from IBM Cloud Pak for Multicloud Management first you need to publish the service from IBM Cloud Automation Manager. Once published, navigate to Automate Infrastructure > Service Library and fill the following input parameters and install the service.

| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---        |
| cloud_connection                | cloudconnection | Name of the IBM cloud connection used to deploy the ROKS cluster. |
| cluster_name                    | string          | Name of the ROKS cluster. Cluster name can have lower case alphabets, numbers and dash. Must start with lower case alphabet and end with alpha-numeric character. Maximum length is 32 characters. |
| OpenShift Container Platform Login Information     | sharedparameter | Details of the OCP on which RHACM enabled IBM CP4MMCM is installed. This newly created cluster will be registered to this RHACM and IBM CP4MCM. Pointing to a data object created from the [oc_login_info](https://github.com/IBM-CAMHub-Open/template_import_rhacm/blob/5.1.0/terraform12/datatypes/ocp.json) data type| |
| cluster_endpoint                | string | URL for the target Kubernetes cluster endpoint |
| cluster_user                    | string | Username for accessing the target Kubernetes cluster |
| cluster_token                   | string | Token for authenticating with the target Kubernetes cluster |
| image_registry                  | URL for private docker registry from which klusterlet images will be pulled | |
| image_suffix                    | Suffix (e.g. -amd64), corresponding to the platform type, to be appended to image name | |
| image_version                   | Version/Tag (e.g 2.0.0 or latest) of the MCM image to be pulled | |
| docker_user                     | Username for authenticating with the private docker registry | |
| docker_password                 | Password for authenticating with the private docker registry | |


### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0
 