# Google Kubernetes Engine Cluster Imported into Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management

## Overview
![alt text](./MCMonGKE.jpg)

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration first uses the [Google Cloud provider](https://www.terraform.io/docs/providers/google/index.html) to provision a kubernetes cluster within the [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine).  Once provisioned, the kubernetes cluster will be imported into the [Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) 2.0.0 hub-cluster to make it a managed cluster.

More details on IBM Cloud Automation Manager Service can be found [here](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html).

This service is composed of following terraform templates

- [Google Kubernetes Engine for Terraform 0.12.x](https://github.com/IBM-CAMHub-Open/template_kubernetes_gke/tree/1.11) terraform template.
- [Import Google Kubernetes Engine cluster into RHACM enabled IBM CP4MCM](https://github.com/IBM-CAMHub-Open/template_import_rhacm/tree/5.1.0/terraform12/GKE/mcm-klusterlet) terraform template 


This service can be either deployed from IBM Cloud Automation Manager or from IBM Cloud Pak for Multicloud Management Catalog.

* [Deploying the service from IBM Cloud Automation Manager](#deploying-the-service-from-ibm-cloud-automation-manager)
* [Deploying the service from IBM Cloud Pak for Multicloud Management Service Library](#deploying-the-service-from-ibm-cloud-private-catalog)

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > Google Kubernetes Engine Cluster with RHACM import. Fill the following input parameters and deploy the service.

| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---                  |
| cloud_connection                | connection      | Name of the Google cloud connection used to deploy the GKE cluster. |
| cluster_name                    | string          | Name of the GKE cluster. Cluster name can have lower case alphabets, numbers and dash. Must start with lower case alphabet and end with alpha-numeric character. Maximum length is 32 characters. |
| kube_version                    | string          | Kubernetes version for the cluster. Specify 'latest' for the most recent kubernetes version supported by the Kubernetes Service, or a version number in the X.Y[.Z] format (e.g. 1.13 or 1.13.5).  The most recent maintenance release for the specified version will be selected. |
| service\_account\_key           | string          | JSON-formatted key for admin service account associated with cluster, Base64 encoded |
| OpenShift Container Platform Login Information     | sharedparameter | Details of the OCP on which RHACM enabled IBM CP4MMCM is installed. This newly created cluster will be registered to this RHACM and IBM CP4MCM. Pointing to a data object created from the [oc_login_info](https://github.com/IBM-CAMHub-Open/template_import_rhacm/blob/5.1.0/terraform12/datatypes/ocp.json) data type| |
| zone                            | string          | Zone within the cloud in which to create the cluster |
| machine_type                    | string          | Machine type for worker nodes |
| disk\_size\_gb                  | string          | Size of the worker node disk |
| disk_type                       | string          | Type of the worker node disk |
| initial\_worker\_count          | string          | Initial number of worker nodes |
| min\_worker\_count              | string          | Minimum number of worker nodes |
| max\_worker\_count              | string          | Maximum number of worker nodes |



## Deploying the service from IBM Cloud Pak for Multicloud Management Service Library

To deploy this service from IBM Cloud Pak for Multicloud Management first you need to publish the service from IBM Cloud Automation Manager. Once published, navigate to Automate Infrastructure > Service Library and fill the following input parameters and install the service.

Note: Some parameters may have fixed default values.  If you need to change them, make a copy of this service configuration and create a new service in IBM Cloud Automation Manager with the new configuration. 

| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---                  |
| cloud_connection                | connection      | Name of the Google cloud connection used to deploy the GKE cluster. |
| cluster_name                    | string          | Name of the GKE cluster |
| kube_version                    | string          | Kubernetes version for the cluster. Specify 'latest' for the most recent kubernetes version supported by the Kubernetes Service, or a version number in the X.Y[.Z] format (e.g. 1.13 or 1.13.5).  The most recent maintenance release for the specified version will be selected. |
| service\_account\_key           | string          | JSON-formatted key for admin service account associated with cluster, Base64 encoded |
| OpenShift Container Platform Login Information     | sharedparameter | Details of the OCP on which RHACM enabled IBM CP4MMCM is installed. This newly created cluster will be registered to this RHACM and IBM CP4MCM. Pointing to a data object created from the [oc_login_info](https://github.com/IBM-CAMHub-Open/template_import_rhacm/blob/5.1.0/terraform12/datatypes/ocp.json) data type| |
| zone                            | string          | Zone within the cloud in which to create the cluster |
| machine_type                    | string          | Machine type for worker nodes |
| disk\_size\_gb                  | string          | Size of the worker node disk |
| disk_type                       | string          | Type of the worker node disk |
| initial\_worker\_count          | string          | Initial number of worker nodes |
| min\_worker\_count              | string          | Minimum number of worker nodes |
| max\_worker\_count              | string          | Maximum number of worker nodes |


### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0