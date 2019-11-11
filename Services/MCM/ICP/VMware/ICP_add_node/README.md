# ICP cluster add node

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/en/SS2L37/product_welcome_cloud_automation_manager.html) service configuration uses the [VMware provider](https://www.terraform.io/docs/providers/vsphere/index.html) or [OpenStack provider](https://www.terraform.io/docs/providers/openstack/index.html) to provision virtual machines on VMware 
or Openstack, and deploys additional [IBM Cloud Private](https://www.ibm.com/cloud-computing/products/ibm-cloud-private/) 3.2.1 node to an existing ICP deployment. Using this service you can add one of the
following nodes

* Worker
* Proxy
* Management
* Vulnerability Advisor (VA)
	
This service makes use of the following [template](https://github.com/IBM-CAMHub-Open/template_icp_node/tree/3.2.1) 
to standup the additional node.

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > Cluster Lifecycle Services > ICP cluster add node. Fill the following input parameters and deploy the service.

### Parameters required for adding a node to VMware

The service for VMware add node makes use of the following data type. Data objects for this types must be 
created before deploying this service. 

* [vSphere Managed Inventory Definition](https://github.com/IBM-CAMHub-Open/template_cam_common/blob/3.2.1/common/datatypes/vsphere_inventory.json) -  vSphere Managed Inventory Objects that are used in virtual machine creation.

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| Boot node IPv4 address | | Boot node IP address of the existing cluster |
| Master node IPv4 address | | Master node IP address of the existing cluster |
| ICP cluster location | /root/ibm-cloud-private-x86_64-3.2.1/cluster | Install location of ICP on boot node |
| ICP cluster node type | Worker | Node type to add. Select a node type from the drop down list |
| Domain | | Node domain name |
| Root user | | OS Root User name |
| Root password| | OS Root password |
| Node Hostname and IPv4 address | | New node's hostname and IP address |
| Node memory | 16384 | Memory for the new node |
| Node vCPU | 16 | vCPU for the new node |
| Node disk1 size | 200 |  Disk size of the new node |
| Enable GlusterFS | | Select true to enable GlusterFS on the worker node, false otherwise. Valid only if node type is Worker |
| Node disk2 size | | Second disk size of the new node |

### Parameters required for adding a node to OpenStack
| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| Boot node IPv4 address | | Boot node IP address of the existing cluster |
| Master node IPv4 address | | Master node IP address of the existing cluster |
| ICP cluster location | /root/ibm-cloud-private-x86_64-3.2.1/cluster | Install location of ICP on boot node |
| ICP cluster node type | Worker | Node type to add. Select a node type from the drop down list |
| Domain | | Node domain name |
| Root user | | OS Root User name |
| Root password| | OS Root password |
| Node Hostname and IPv4 address | | New node's hostname and IP address |
| Node disk1 size | 200 |  Disk size of the new node |
| Enable GlusterFS | | Select true to enable GlusterFS on the worker node, false otherwise. Valid only if node type is Worker |
| Node disk2 size | | Second disk size of the new node |
| Security groups | | OpenStack security group |
| Public IPv4 pool | | OpenStack network name |
| Image ID | | OpenStack image ID|
| VM flavour id | | OpenStack flavor id for this node |
