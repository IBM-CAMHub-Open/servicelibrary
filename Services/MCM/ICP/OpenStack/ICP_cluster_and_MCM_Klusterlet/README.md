# ICP Deployment with klusterlet on OpenStack

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/en/SS2L37/product_welcome_cloud_automation_manager.html) service configuration first uses the [OpenStack provider](https://www.terraform.io/docs/providers/openstack/index.html) to provision virtual machines on OpenStack and deploys [IBM Cloud Private](https://www.ibm.com/cloud-computing/products/ibm-cloud-private/) 3.2.0 on them. This configuration then imports the deployed ICP to [IBM Multicloud Manager](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.2.0/mcm/getting_started/introduction.html) Controller to be managed by the controller. 

More details on IBM Cloud Automation Manager Service can be found [here](https://www.ibm.com/support/knowledgecenter/en/SS2L37_3.2.1.0/cam_managing_services.html).

Using this service you can deploy ICP in either Single, Medium or HA topology. Single topology will install all
the ICP nodes in a single virtual machine. Medium topology is meant for having multiple worker nodes. HA toplogy
allows multiple master and proxy with virtual IP, and multiple worker nodes.

This service is composed of following terraform templates

* ICP OpenStack template
	* [IBM Cloud Private HA Node Installation](https://github.com/IBM-CAMHub-Open/template_icp_installer) terraform template.
	* [IBM Cloud Private Medium Setup Installation](https://github.com/IBM-CAMHub-Open/template_icp_installer_medium) terraform template.
	* [IBM Cloud Private Single Node Installation](https://github.com/IBM-CAMHub-Open/template_icp_installer_single) terraform template.
	
* [IBM Multicloud Manager 3.2.0](https://github.com/IBM-CAMHub-Open/template_mcm_install/tree/3.2.0/ICP/terraform) terraform template.

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > Cluster Lifecycle Services > ICP cluster v3_2_0 on OpenStack. Fill the following input parameters and deploy the service.

### Parameters for Single node cluster

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| Single Node VM Flavour id | | OpenStack flavor that defines the compute and memory capacity of ICP single node topology.|
| Hostname and IP address | | Hostname and IPv4 address for single node VM. |
| VM OS user | root | Template OS root user for ICP nodes. |
| VM OS password | | OS root password for ICP nodes. |
| Domain name |  | Virtual Machine Domain name. |
| Single Node VM disk size | | Storage capacity of ICP Single node. |
| VM Image ID | | OpenStack Image ID to be used for ICP Single node. |
| VM security groups |  | OpenStack security group. |
| Docker binary URL |  | URL to download docker binary (URL in http, https, ftp and file protocol). |
| ICP binary download URL |  | URL to download ICP binary (URL in http, https, ftp and file protocol). |
| ICP console admin user | admin | ICP admin user name. |
| ICP console Admin password |  | ICP admin user password. Allows alphanumeric characters or - symbol. Must have at least 32 characters. |
| Enable Kibana | True | Select true to enable kibana on ICP cluster, false otherwise. |
| Enable Monitoring | True | Select true to enable monitoring on ICP cluster, false otherwise. |
| Enable Metering | False | Select true to enable metering on ICP cluster, false otherwise. |
| ICP Cluster Name | mycluster | ICP Cluster Name |
| VM Public IPv4 pool | | OpenStack network name |
| IBM MCM Controller Definition | | Dataobject that contains IBM MCM Controller (hub cluster) details. The ICP deployed by this service will imported to the selected controller. |

### Parameters for Medium topology

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| VM OS user | root | Template OS root user for ICP nodes. |
| VM OS password | | OS root password for ICP nodes. |
| Domain name |  | Virtual Machine Domain name. |
| VM Image ID | | OpenStack Image ID to be used for ICP Single node. |
| VM security groups |  | OpenStack security group. |
| Docker binary URL |  | URL to download docker binary (URL in http, https, ftp and file protocol). |
| ICP binary download URL |  | URL to download ICP binary (URL in http, https, ftp and file protocol). |
| ICP console admin user | admin | ICP admin user name. |
| ICP console Admin password |  | ICP admin user password. Allows alphanumeric characters or - symbol. Must have at least 32 characters. |
| Enable Kibana | True | Select true to enable kibana on ICP cluster, false otherwise. |
| Enable Monitoring | True | Select true to enable monitoring on ICP cluster, false otherwise. |
| Enable Metering | False | Select true to enable metering on ICP cluster, false otherwise. |
| ICP Cluster Name | mycluster | ICP Cluster Name |
| VM Public IPv4 pool | | OpenStack network name |
| IBM MCM Controller Definition | | Dataobject that contains IBM MCM Controller (hub cluster) details. The ICP deployed by this service will imported to the selected controller. |
| Boot Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP boot node.|
| Boot node Hostname and IPv4 address | | Hostname and IPv4 address for boot node VM. |
| Boot Node VM disk size | 200 | Storage capacity of ICP Boot node. |
| Master Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP master node.|
| Master node Hostname and IPv4 address | | Hostname and IPv4 address for master node VM. |
| Master Node VM disk size | 300 | Storage capacity of ICP Master node. |
| Worker Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP worker node.|
| Worker node Hostname and IPv4 address | | Hostname and IPv4 address for worker node VM. |
| Worker Node VM disk1 size | 200 | Storage capacity of ICP Worker node. |
| Worker Node VM disk2 size | | Storage capacity of ICP Worker node. |
| Worker enable glusterFS | false | Select true to enable Gluster FS on worker node, false otherwise. |
| Enable VM management | false | Select true to create management node, false otherwise. |
| Management Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP management node.|
| Management node Hostname and IPv4 address | | Hostname and IPv4 address for management node VM. |
| Management Node VM disk size | 200 | Storage capacity of ICP Management node. |
| Enable VA | false | Select true to create VA node, false otherwise. |
| VA Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP VA node.|
| VA node Hostname and IPv4 address | | Hostname and IPv4 address for VA node VM. |
| VA Node VM disk size | 150 | Storage capacity of ICP VA node. |
| Proxy Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP Proxy node.|
| Proxy node Hostname and IPv4 address | | Hostname and IPv4 address for Proxy node VM. |
| Proxy Node VM disk size | 200 | Storage capacity of ICP Proxy node. |
| Enable NFS | false | Select true to create NFS node for PV, false otherwise. |
| NFS Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP NFS node.|
| NFS node Hostname and IPv4 address | | Hostname and IPv4 address for NFS node VM. |
| NFS Node VM disk1 size | 150 | Storage capacity of ICP NFS node. |
| NFS Node VM disk2 size | 100 | Storage capacity of ICP NFS node. |

### Parameters for HA topology

| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| VM OS user | root | Template OS root user for ICP nodes. |
| VM OS password | | OS root password for ICP nodes. |
| Domain name |  | Virtual Machine Domain name. |
| VM Image ID | | OpenStack Image ID to be used for ICP Single node. |
| VM security groups |  | OpenStack security group. |
| Docker binary URL |  | URL to download docker binary (URL in http, https, ftp and file protocol). |
| ICP binary download URL |  | URL to download ICP binary (URL in http, https, ftp and file protocol). |
| ICP console admin user | admin | ICP admin user name. |
| ICP console Admin password |  | ICP admin user password. Allows alphanumeric characters or - symbol. Must have at least 32 characters. |
| Enable Kibana | True | Select true to enable kibana on ICP cluster, false otherwise. |
| Enable Monitoring | True | Select true to enable monitoring on ICP cluster, false otherwise. |
| Enable Metering | False | Select true to enable metering on ICP cluster, false otherwise. |
| ICP Cluster Name | mycluster | ICP Cluster Name |
| VM Public IPv4 pool | | OpenStack network name |
| IBM MCM Controller Definition | | Dataobject that contains IBM MCM Controller (hub cluster) details. The ICP deployed by this service will imported to the selected controller. |
| Boot Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP boot node.|
| Boot node Hostname and IPv4 address | | Hostname and IPv4 address for boot node VM. |
| Boot Node VM disk size | 200 | Storage capacity of ICP Boot node. |
| Master Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP master node.|
| Master node Hostname and IPv4 address | | Hostname and IPv4 address for master node VM. |
| Master Node VM disk size | 300 | Storage capacity of ICP Master node. |
| Worker Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP worker node.|
| Worker node Hostname and IPv4 address | | Hostname and IPv4 address for worker node VM. |
| Worker Node VM disk1 size | 200 | Storage capacity of ICP Worker node. |
| Worker Node VM disk2 size | | Storage capacity of ICP Worker node. |
| Worker enable glusterFS | false | Select true to enable Gluster FS on worker node, false otherwise. |
| Enable VM management | false | Select true to create management node, false otherwise. |
| Management Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP management node.|
| Management node Hostname and IPv4 address | | Hostname and IPv4 address for management node VM. |
| Management Node VM disk size | 200 | Storage capacity of ICP Management node. |
| Enable VA | false | Select true to create VA node, false otherwise. |
| VA Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP VA node.|
| VA node Hostname and IPv4 address | | Hostname and IPv4 address for VA node VM. |
| VA Node VM disk size | 150 | Storage capacity of ICP VA node. |
| Proxy Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP Proxy node.|
| Proxy node Hostname and IPv4 address | | Hostname and IPv4 address for Proxy node VM. |
| Proxy Node VM disk size | 200 | Storage capacity of ICP Proxy node. |
| Enable NFS | false | Select true to create NFS node for PV, false otherwise. |
| NFS Node VM flavour ID | | OpenStack flavor that defines the compute and memory capacity of ICP NFS node.|
| NFS node Hostname and IPv4 address | | Hostname and IPv4 address for NFS node VM. |
| NFS Node VM disk1 size | 150 | Storage capacity of ICP NFS node. |
| NFS Node VM disk2 size | 100 | Storage capacity of ICP NFS node. |
| ICP cluster vIP |  | Virtual IP address to be used for master nodes |
| ICP cluster vIP interface |  | Interface to set the master node Virtual IP |
| Proxy vIP| | Virtual IP address to be used for prxy nodes |
| Proxy vIP interface | | Interface to set the proxy node Virtual IP |


Copyright IBM Corp. 2019

Service Version - 3.2.0  
 