# IBM Kubernetes Service Cluster Imported into IBM Multicloud Manager

## Overview
![alt text](./MCMonIKS.jpg)

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/en/SS2L37/product_welcome_cloud_automation_manager.html) service configuration first uses the [IBM Cloud provider](https://ibm-cloud.github.io/tf-ibm-docs/v0.17.2/) to provision a kubernetes cluster within the [IBM Kubernetes Service](https://www.ibm.com/cloud/container-service).  Once provisioned, the kubernetes cluster will be imported into the [IBM Multicloud Manager](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.2.0/mcm/getting_started/introduction.html) 3.2.0 hub-cluster to make it a managed cluster.

More details on IBM Cloud Automation Manager Service can be found [here](https://www.ibm.com/support/knowledgecenter/en/SS2L37_3.2.1.0/cam_managing_services.html).

This service is composed of following terraform templates

- [Managed Kubernetes Service within IBM Cloud](https://github.com/IBM-CAMHub-Open/template_kubernetes_iks/tree/1.11) terraform template.
- [MCM Klusterlet 3.2.0 within IBM Cloud Kubernetes Service](https://github.com/IBM-CAMHub-Open/template_mcm_install/tree/3.2.0/IKS/mcm-klusterlet) terraform template 


This service can be either deployed from IBM Cloud Automation Manager or from IBM Cloud Private Catalog.

* [Deploying the service from IBM Cloud Automation Manager](#deploying-the-service-from-ibm-cloud-automation-manager)
* [Deploying the service from IBM Cloud Private Catalog](#deploying-the-service-from-ibm-cloud-private-catalog)

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > MCM on IKS > Deploy and import IKS cluster. Fill the following input parameters and deploy the service.

Note: The parameters indicated as _(hidden)_ have default values.  If you need to change them, make a copy of this service configuration and create a new service in IBM Cloud Automation Manager with the new configuration. 

| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---        |
| cluster_name                    | string          | Name of the IKS cluster |
| kube_version                    | string          | Kubernetes version for the cluster. Specify 'latest' for the most recent kubernetes version supported by the Kubernetes Service, or a version number in the X.Y[.Z] format (e.g. 1.13 or 1.13.5).  The most recent maintenance release for the specified version will be selected. |
| MCM Controller Data Object      | sharedparameter |Details of the MCM controller this newly created cluster will be registered with. Pointing to a data object created from the [mcm_controller](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/mcm_controller.json) data type|
| region                          | string          | _(hidden)_ Region in which to create the cluster |
| org                             | string          | _(hidden)_ IBM Cloud org name |
| space                           | string          | _(hidden)_ IBM Cloud space name |
| resource\_group\_name           | string          | _(hidden)_ Name of the resource group in which the cluster will be created |
| private\_vlan\_id               | string          | _(hidden)_ ID for the cluster's private VLAN |
| public\_vlan\_id                | string          | _(hidden)_ ID for the cluster's public VLAN |
| subnet_id                       | string          | _(hidden)_ ID for cluster's subnet |
| num_workers                     | string          | _(hidden)_ Number of worker nodes in the cluster |
| datacenter                      | string          | _(hidden)_ Datacenter in which to create the cluster |
| machine_type                    | string          | _(hidden)_ Identifier for the VM type/configuration (CPU count, memory, network and speed) |


## Deploying the service from IBM Cloud Private Catalog

To deploy this service from IBM Cloud Private Catalog navigate to Catalog, search the Catalog for deploy-and-import-iks-cluster and fill the following input parameters and install the service.

Note: The parameters indicated as _(hidden)_ have default values.  If you need to change them, make a copy of this service configuration and create a new service in IBM Cloud Automation Manager with the new configuration. 

| Parameter name                  | Type            | Parameter description |
| :---                            | :---            | :---        |
| cluster_name                    | string          | Name of the IKS cluster |
| kube_version                    | string          | Kubernetes version for the cluster. Specify 'latest' for the most recent kubernetes version supported by the Kubernetes Service, or a version number in the X.Y[.Z] format (e.g. 1.13 or 1.13.5).  The most recent maintenance release for the specified version will be selected. |
| MCM Controller Data Object      | sharedparameter |Details of the MCM controller this newly created cluster will be registered with. Pointing to a data object created from the [mcm_controller](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/mcm_controller.json) data type|
| region                          | string          | _(hidden)_ Region in which to create the cluster |
| org                             | string          | _(hidden)_ IBM Cloud org name |
| space                           | string          | _(hidden)_ IBM Cloud space name |
| resource\_group\_name           | string          | _(hidden)_ Name of the resource group in which the cluster will be created |
| private\_vlan\_id               | string          | _(hidden)_ ID for the cluster's private VLAN |
| public\_vlan\_id                | string          | _(hidden)_ ID for the cluster's public VLAN |
| subnet_id                       | string          | _(hidden)_ ID for cluster's subnet |
| num_workers                     | string          | _(hidden)_ Number of worker nodes in the cluster |
| datacenter                      | string          | _(hidden)_ Datacenter in which to create the cluster |
| machine_type                    | string          | _(hidden)_ Identifier for the VM type/configuration (CPU count, memory, network and speed) |


### License and Maintainer

Copyright IBM Corp. 2019

Service Version - 3.2.0  
 