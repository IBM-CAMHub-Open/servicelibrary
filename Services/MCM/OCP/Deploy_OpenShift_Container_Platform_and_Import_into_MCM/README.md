# OpenShift Container Platform 3.11 cluster on VMware 

## Overview
This service deploys OpenShift Container Platform (OCP) cluster version 3.11 on VMware and imports it into an existing IBM Multi Cloud Manager (MCM) controller.


## Supported topologies
![alt text](./OCP.jpg)

The service contains a decision points which allows customers to chose one of the following two OCP topologies: 
1. [OpenShift Container Platform Single Node Installation](https://github.com/IBM-CAMHub-Open/template_openshift_installer_single/tree/3.11) In this topology, a single node is deployed and all OCP services are deployed on that single node. Refer to the template documentation for more details.


2. [OpenShift Container Platform Enterprise Installation](https://github.com/IBM-CAMHub-Open/template_openshift_installer/tree/3.11)
In this topology, each one of the following services can have its own dedicated node: 
 - master (one or more)
 - lb (optional)
 - etcd (can be combined with the master node if the provided hostname and IP are the same)
 - infra (one)
 - compute (one or more. At least 3 nodes if glusterFS is enabled)
 Refer to the template documentation for more details.

The second activity of the service is the terraform template that performs an MCM import which will register the newly deployed MCM cluster with an existing MCM controller(hub)

## Service input
The following service plans are defined:
 - ### OpenShift Container Platform - single node

| Parameter Name | Type | Description |
| ----- | ----------| ----- |
| VMware Cloud Connection Name | cloudconnection | Name of the VMware cloud connection used to deploy the OpenShift Container Platform|
| OpenShift Admin User Name|string|Name of the cluster admin user that will be created on OpenShift|
| OpenShift Admin Password|password|Password for the OpenShift cluster admin user that will be created|
| RedHat Subscription Data Object|sharedparameter|RedHat Subscription used on the cluster nodes. Pointing to a data object created from the [redhat_subscription](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/redhat_subscription.json) data type|
| vSphere Managed Inventory Definition Data Object|sharedparameter|vSphere Managed Inventory Definition. Pointing to a data object created from the [vsphere_managed_inventory_definition](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/vsphere_inventory.json) data type|
| OpenShift Container Platform Single Node on VMware Data Object|sharedparameter|Pointing to a data object created from the [openshift_single_node_on_vmware](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/openshift_single_node_on_vmware.json) data type|
|MCM Controller Data Object|sharedparameter|Details of the MCM controller this newly created cluster will be registered with. Pointing to a data object created from the [mcm_controller](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/mcm_controller.json) data type|
|Single Node Hostname and IP|map|Single Node Hostname and IP address|


 - ### OpenShift Container Platform - multi node

| Parameter Name | Type | Description |
| ----- | ----------| ----- |
| VMware Cloud Connection Name | cloudconnection | Name of the VMware cloud connection used to deploy the OpenShift Container Platform|
| OpenShift Admin User Name|string|Name of the cluster admin user that will be created on OpenShift|
| OpenShift Admin Password|password|Password for the OpenShift cluster admin user that will be created|
| RedHat Subscription Data Object|sharedparameter|RedHat Subscription used on the cluster nodes. Pointing to a data object created from the [redhat_subscription](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/redhat_subscription.json) data type|
| vSphere Managed Inventory Definition Data Object|sharedparameter|vSphere Managed Inventory Definition. Pointing to a data object created from the [vsphere_managed_inventory_definition](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/vsphere_inventory.json) data type|
| OpenShift Container Platform Master Node on VMware Data Object|sharedparameter|Pointing to a data object created from the [openshift_master_node_on_vmware](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/openshift_master_node_on_vmware.json) data type|
| OpenShift Container Platform LB Node on VMware Data Object|sharedparameter|Pointing to a data object created from the [openshift_lb_node_on_vmware](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/openshift_lb_node_on_vmware.json) data type|
| OpenShift Container Platform Infrastructure Node on VMware Data Object|sharedparameter|Pointing to a data object created from the [openshift_infra_node_on_vmware](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/openshift_infra_node_on_vmware.json) data type|
| OpenShift Container Platform ETCD Node on VMware Data Object|sharedparameter|Pointing to a data object created from the [openshift_etcd_node_on_vmware](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/openshift_etcd_node_on_vmware.json) data type|
| OpenShift Container Platform Compute Node on VMware Data Object|sharedparameter|Pointing to a data object created from the [openshift_compute_node_on_vmware](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/openshift_compute_node_on_vmware.json) data type|
|MCM Controller Data Object|sharedparameter|Details of the MCM controller this newly created cluster will be registered with. Pointing to a data object created from the [mcm_controller](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/mcm_controller.json) data type|
|Master Node Hostname and IP|map|Master Node Hostname and IP address |
|ETCD Node Hostname and IP|map|ETCD Node Hostname and IP address. If the hostname and IP are the same as the master node, the ETCD service will be deployed on the master node |
|Infrastructure Node Hostname and IP|map|Infrastructure Node Hostname and IP address|
|LB Node Hostname and IP|map|LB Node Hostname and IP. Optional|
|Compute Node Hostname and IP|map|Compute Node Hostname and IP address. One or more. For GlusterFS, at least 3 compute nodes are required|
|Enable Load Balancer|string|Indicates wether a load balancer will be deployed with the cluster. Defaults to true.|

### License and Maintainer

Copyright IBM Corp. 2019

Service Version - 3.2.0  