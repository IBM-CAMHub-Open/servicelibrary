# Existing kubernetes cluster imported into Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management

## Overview
![alt text](./MCMonROKS.jpg)

This service imports an existing kubernetes cluster into the [Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) 2.x hub-cluster to make it a managed cluster.

More details on IBM Cloud Pak for Multicloud Management Services can be found [here](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html).

This service is composed of following terraform templates

- [Import a kubernetes cluster into RHACM enabled IBM CP4MCM](https://github.com/IBM-CAMHub-Open/template_import_rhacm/tree/5.1.0/terraform12/other/mcm-klusterlet) terraform template.


You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. 
By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

* [Test Deploy the Service](#test-deploy-the-service)
* [Deploying the service from Service Library](#deploying-the-service-from-service-library)

## Test Deploy the Service

To test deploy this service navigate to Automate Infrastructure > Manage Services > Import a kubernetes cluster into RHACM enabled IBM CP4MCM. Fill the following input parameters and deploy the service.


| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---        |
| cloud_connection                | cloudconnection | Name of the IBM cloud connection used to deploy the ROKS cluster. |
| cluster_name                    | string          | Name of the ROKS cluster. Cluster name can have lower case alphabets, numbers and dash. Must start with lower case alphabet and end with alpha-numeric character. Maximum length is 32 characters. |
| OpenShift Container Platform Login Information     | sharedparameter | Details of the OCP on which RHACM enabled IBM CP4MMCM is installed. This newly created cluster will be registered to this RHACM and IBM CP4MCM. Pointing to a data object created from the [oc_login_info](https://github.com/IBM-CAMHub-Open/template_import_rhacm/blob/5.1.0/terraform12/datatypes/ocp.json) data type| |
| cluster_endpoint                | string | URL for the target Kubernetes cluster endpoint |
| cluster_user                    | string | Username for accessing the target Kubernetes cluster |
| cluster_token                   | string | Token for authenticating with the target Kubernetes cluster |
| kube_ctl_version                | string          | The kubectl version to use in import client. For compatibility reasons, this version must match the version in the kubernetes service. The latest client version may not be compatible with the latest kubernetes version used in the server. It is recommended that you set an explicit version. Version format must be vM.m.p eg. v1.23.6. | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

Note: Some parameters may have fixed default values. If you need to change them, duplicate the service configuration and create a new service with the new configuration. 

| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---        |
| cloud_connection                | cloudconnection | Name of the IBM cloud connection used to deploy the ROKS cluster. |
| cluster_name                    | string          | Name of the ROKS cluster. Cluster name can have lower case alphabets, numbers and dash. Must start with lower case alphabet and end with alpha-numeric character. Maximum length is 32 characters. |
| OpenShift Container Platform Login Information     | sharedparameter | Details of the OCP on which RHACM enabled IBM CP4MMCM is installed. This newly created cluster will be registered to this RHACM and IBM CP4MCM. Pointing to a data object created from the [oc_login_info](https://github.com/IBM-CAMHub-Open/template_import_rhacm/blob/5.1.0/terraform12/datatypes/ocp.json) data type| |
| cluster_endpoint                | string | URL for the target Kubernetes cluster endpoint |
| cluster_user                    | string | Username for accessing the target Kubernetes cluster |
| cluster_token                   | string | Token for authenticating with the target Kubernetes cluster |
| kube_ctl_version                | string          | The kubectl version to use in import client. For compatibility reasons, this version must match the version in the kubernetes service. The latest client version may not be compatible with the latest kubernetes version used in the server. It is recommended that you set an explicit version. Version format must be vM.m.p eg. v1.23.6. | |
### License and Maintainer

Copyright IBM Corp. 2022

Service Version - 2.0.0.0
 