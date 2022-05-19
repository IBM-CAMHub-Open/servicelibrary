# Google Kubernetes Engine Cluster Imported into Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management

## Overview
![alt text](./MCMonGKE.jpg)

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration first uses the [Google Cloud provider](https://www.terraform.io/docs/providers/google/index.html) to provision a kubernetes cluster within the [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine).  Once provisioned, the kubernetes cluster will be imported into the [Red Hat Advanced Cluster Management enabled IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) 2.x hub-cluster to make it a managed cluster.

This service is composed of following terraform templates

- [Google Kubernetes Engine for Terraform 0.12.x](https://github.com/IBM-CAMHub-Open/template_kubernetes_gke/tree/1.11) terraform template.
- [Import Google Kubernetes Engine cluster into RHACM enabled IBM CP4MCM](https://github.com/IBM-CAMHub-Open/template_import_rhacm/tree/5.1.0/terraform12/GKE/mcm-klusterlet) terraform template 


You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. 
By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

* [Test Deploy the Service](#test-deploy-the-service)
* [Deploying the service from Service Library](#deploying-the-service-from-service-library)

## Test Deploy the Service

To test deploy this service navigate to Automate Infrastructure > Manage Services > Google Kubernetes Engine Cluster with RHACM import. Fill the following input parameters and deploy the service.

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
| kube_ctl_version                | string          | The kubectl version to use in import client. For compatibility reasons, this version must match the version in the kubernetes service. The latest client version may not be compatible with the latest kubernetes version used in the server. It is recommended that you set an explicit version. Version format must be vM.m.p eg. v1.23.6. | |


## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

Note: Some parameters may have fixed default values. If you need to change them, duplicate the service configuration and create a new service with the new configuration. 

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
| kube_ctl_version                | string          | The kubectl version to use in import client. For compatibility reasons, this version must match the version in the kubernetes service. The latest client version may not be compatible with the latest kubernetes version used in the server. It is recommended that you set an explicit version. Version format must be vM.m.p eg. v1.23.6. | |

### License and Maintainer

Copyright IBM Corp. 2022

Service Version - 2.0.0.0