# ICP cluster add node

This [IBM Cloud Automation Manager](https://www.ibm.com/support/knowledgecenter/en/SS2L37/product_welcome_cloud_automation_manager.html) service configuration upgrades an ICP 3.1.2 
deployment on VMware or OpenStack to ICP 3.2.0.
	
This service makes use of the following [template](https://github.com/IBM-CAMHub-Open/template_icp_upgrade/tree/3.2.0/ICP/terraform) 
to upgrade ICP from 3.1.2 to 3.2.0.

## Deploying the service from IBM Cloud Automation Manager

To deploy this service from IBM Cloud Automation Manager navigate to Library > Services > Cluster Lifecycle Services > ICP cluster upgrade. Fill the following input parameters and deploy the service.

### Parameters required for upgrading ICP


| Parameter | Default Value | Description |
| :-------------- |:--------------| :-----|
| Boot node IPv4 address | | Boot node IP address of the existing cluster |
| Master node IPv4 address | | Master node IP address of the existing cluster |
| ICP cluster folder location | /root/ibm-cloud-private-x86_64-3.1.2/cluster | Install location of existing ICP version on boot node |
| New ICP binary URL | | URL location of ICP 3.2.0 binary. The location must be in http/https/ftp/file URL format. |
| Boot node root user | | Boot node OS Root User name |
| Boot node root password| | Boot node OS Root password |
| ICP cluster | mycluster.icp | ICP cluster name.  |
| Kube apiserver secure port | 8001 | ICP Kubernetes API Port |
| Cloud Connection |  | Connection to the existing ICP cluster |