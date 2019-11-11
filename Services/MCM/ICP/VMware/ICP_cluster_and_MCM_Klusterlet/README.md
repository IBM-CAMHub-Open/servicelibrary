# ICP Deployment with klusterlet on VMware

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/en/SS2L37/product_welcome_cloud_automation_manager.html) service configuration first uses the [VMware provider](https://www.terraform.io/docs/providers/vsphere/index.html) to provision virtual machines on VMware and deploys [IBM Cloud Private](https://www.ibm.com/cloud-computing/products/ibm-cloud-private/) 3.2.1 on them. This configuration then imports the deployed ICP to [IBM Multicloud Manager](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.2.1/mcm/getting_started/introduction.html) Controller to be managed by the controller. 

More details on IBM Cloud Automation Manager Service can be found [here](https://www.ibm.com/support/knowledgecenter/en/SS2L37_3.2.1.0/cam_managing_services.html).

Using this service you can deploy ICP in either Single, Medium or HA topology. Single topology will install all
the ICP nodes in a single virtual machine. Medium topology is meant for having multiple worker nodes. HA toplogy
allows multiple master and proxy with virtual IP, and multiple worker nodes.

This service is composed of following terraform templates

* ICP VMware template
	* [IBM Cloud Private HA Node Installation](https://github.com/IBM-CAMHub-Open/template_icp_installer) terraform template.
	* [IBM Cloud Private Medium Setup Installation](https://github.com/IBM-CAMHub-Open/template_icp_installer_medium) terraform template.
	* [IBM Cloud Private Single Node Installation](https://github.com/IBM-CAMHub-Open/template_icp_installer_single) terraform template.
	
* [IBM Multicloud Manager 3.2.1](https://github.com/IBM-CAMHub-Open/template_mcm_install/tree/3.2.1/ICP/terraform) terraform template.

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > Cluster Lifecycle Services > ICP cluster on VMware. Fill the following input parameters and deploy the service.

This service makes use of the following data types. Data objects for these types must be 
created before deploying this service. 

* [vSphere Managed Inventory Definition](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/vsphere_inventory.json) -  vSphere Managed Inventory Objects that are used in virtual machine creation.
* [IBM MCM Controller Definition](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/mcm_controller.json) - Data structure describing connection details for an IBM Multicloud Manager Controller and its host IBM Cloud Private server.
* [ICP Single node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_single_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP Single Node on VMware. Required for single node ICP deployment.
* [ICP Boot node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_boot_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP Boot Node on VMware. Required for HA and medium ICP deployment.
* [ICP Master node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_master_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP Master Node on VMware. Required for HA and medium ICP deployment.
* [ICP Worker node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_worker_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP Worker Node on VMware. Required for HA and medium ICP deployment.
* [ICP Proxy node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_proxy_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP Proxt Node on VMware. Required for HA and medium ICP deployment.
* [ICP VA node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_va_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP VA Node on VMware. Required for HA and medium ICP deployment.
* [ICP Management node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_mgmt_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP Management Node on VMware. Required for HA and medium ICP deployment.
* [ICP NFS node](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/icp_nfs_node_on_vmware.json) - Defines the compute, memory, and storage capacity of ICP NFS Node on VMware. Required for HA and medium ICP deployment.

### Parameters for Single node cluster

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| vSphere Managed Inventory Definition | | vSphere Managed Inventory Objects that are used in virtual machine creation. |
| ICP Single node | | Dataobject that defines the compute, memory, and storage capacity of ICP single node topology.|
| Single node hostname ip | | Hostname and IPv4 address for single node VM. |
| Template OS root user | root | Template OS root user for ICP nodes. |
| OS root password | passw0rd| OS root password for ICP nodes. |
| Domain name |  | Virtual Machine Domain name. |
| VM clone timeout period | 30 | VM clone timeout period. |
| Docker binary download URL |  | URL to download docker binary (URL in http, https, ftp and file protocol). |
| ICP binary URL |  | URL to download ICP binary (URL in http, https, ftp and file protocol). |
| ICP admin user | admin | ICP admin user name. |
| ICP admin password |  | ICP admin user password. Allows alphanumeric characters or - symbol. Must have at least 32 characters. |
| Enable Kibana | True | Select true to enable kibana on ICP cluster, false otherwise. |
| Enable Monitoring | True | Select true to enable monitoring on ICP cluster, false otherwise. |
| Enable metering | False | Select true to enable metering on ICP cluster, false otherwise. |
| ICP cluster name | mycluster | ICP Cluster Name |
| IBM MCM Controller Definition | | Dataobject that contains IBM MCM Controller (hub cluster) details. The ICP deployed by this service will imported to the selected controller. |

### Parameters for Medium topology

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| vSphere Managed Inventory Definition | | vSphere Managed Inventory Objects that are used in virtual machine creation. |
| ICP Boot Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP boot node topology.|
| Boot node hostname and IPv4 | | Hostname and IPv4 address for boot node VM. |
| ICP Master Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP master node topology.|
| Master node hostname and IPv4 | | Hostname and IPv4 address for master node VM. |
| ICP Worker Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP worker node topology.|
| Worker root node hostname and IPv4 | | Hostname and IPv4 address for worker node VM. |
| ICP Poxy Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP proxy node topology.|
| Poxy node hostname and IPv4 | | Hostname and IPv4 address for proxy node VM. |
| Enable management node | True | Select true to create management node, false otherwise. |
| ICP Management Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP management node topology.|
| Management node hostname and IPv4 | | Hostname and IPv4 address for management node VM. |
| Enable VA node | False | Select true to create VA node, false otherwise. |
| VA Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP VA node topology.|
| VA node hostname and IPv4 | | Hostname and IPv4 address for VA node VM. |
| Enable NFS node | True | Select true to create NFS node, false otherwise. |
| ICP NFS Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP NFS node topology.|
| NFS node hostname and IPv4 | | Hostname and IPv4 address for NFS node VM. |
| Template OS root user | root | Template OS root user for ICP nodes. |
| OS root password | passw0rd| OS root password for ICP nodes. |
| Domain name |  | Virtual Machine Domain name. |
| VM clone timeout period | 30 | VM clone timeout period. |
| Docker binary download URL |  | URL to download docker binary (URL in http, https, ftp and file protocol). |
| ICP binary URL |  | URL to download ICP binary (URL in http, https, ftp and file protocol). |
| ICP admin user | admin | ICP admin user name. |
| ICP admin password |  | ICP admin user password. Allows alphanumeric characters or - symbol. Must have at least 32 characters. |
| Enable Kibana | True | Select true to enable kibana on ICP cluster, false otherwise. |
| Enable Monitoring | True | Select true to enable monitoring on ICP cluster, false otherwise. |
| Enable metering | False | Select true to enable metering on ICP cluster, false otherwise. |
| ICP cluster name | mycluster | ICP Cluster Name |
| IBM MCM Controller Definition | | Dataobject that contains IBM MCM Controller (hub cluster) details. The ICP deployed by this service will imported to the selected controller. |

### Parameters for HA topology

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| vSphere Managed Inventory Definition | | vSphere Managed Inventory Objects that are used in virtual machine creation. |
| ICP Boot Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP boot node topology.|
| Boot node hostname and IPv4 | | Hostname and IPv4 address for boot node VM. |
| ICP Master Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP master node topology.|
| Master node hostname and IPv4 | | Hostname and IPv4 address for master node VM. |
| ICP Worker Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP worker node topology.|
| Worker root node hostname and IPv4 | | Hostname and IPv4 address for worker node VM. |
| ICP Poxy Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP proxy node topology.|
| Poxy node hostname and IPv4 | | Hostname and IPv4 address for proxy node VM. |
| Enable management node | True | Select true to create management node, false otherwise. |
| ICP Management Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP management node topology.|
| Management node hostname and IPv4 | | Hostname and IPv4 address for management node VM. |
| Enable VA node | False | Select true to create VA node, false otherwise. |
| VA Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP VA node topology.|
| VA node hostname and IPv4 | | Hostname and IPv4 address for VA node VM. |
| Enable NFS node | True | Select true to create NFS node, false otherwise. |
| ICP NFS Node Configuration | | Dataobject that defines the compute, memory, and storage capacity of ICP NFS node topology.|
| NFS node hostname and IPv4 | | Hostname and IPv4 address for NFS node VM. |
| Template OS root user | root | Template OS root user for ICP nodes. |
| OS root password | passw0rd| OS root password for ICP nodes. |
| Domain name |  | Virtual Machine Domain name. |
| VM clone timeout period | 30 | VM clone timeout period. |
| Docker binary download URL |  | URL to download docker binary (URL in http, https, ftp and file protocol). |
| ICP binary URL |  | URL to download ICP binary (URL in http, https, ftp and file protocol). |
| ICP admin user | admin | ICP admin user name. |
| ICP admin password |  | ICP admin user password. Allows alphanumeric characters or - symbol. Must have at least 32 characters. |
| Enable Kibana | True | Select true to enable kibana on ICP cluster, false otherwise. |
| Enable Monitoring | True | Select true to enable monitoring on ICP cluster, false otherwise. |
| Enable metering | False | Select true to enable metering on ICP cluster, false otherwise. |
| ICP cluster name | mycluster | ICP Cluster Name |
| ICP cluster VIP |  | Virtual IP address to be used for master nodes |
| ICP cluster vip interface |  | Interface to set the master node Virtual IP |
| Proxy vip| | Virtual IP address to be used for prxy nodes |
| Proxy vip interface | | Interface to set the proxy node Virtual IP |
| IBM MCM Controller Definition | | Dataobject that contains IBM MCM Controller (hub cluster) details. The ICP deployed by this service will imported to the selected controller. |

Copyright IBM Corp. 2019

Service Version - 3.2.1
 
