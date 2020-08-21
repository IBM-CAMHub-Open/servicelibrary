# Single Virtual Machine on VMware

## Overview
![alt text](./VMOnVMware.png)

This [IBM Cloud Pak for Multicloud Management](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html) service configuration uses the [VMware provider](https://www.terraform.io/docs/providers/vsphere/index.html) to provision a Virtual Machine on VMware.

This service is composed of following terraform template

- [SingleVirtualMachine](https://github.com/IBM-CAMHub-Open/starterlibrary/tree/2.4/VMware/terraform/hcl/singleVM) terraform template.

You can first test deploy the service and once satisfied, you can publish the service to the service library and then deploy the production ready service from the service library. 
By default this service is in global namespace. So before you publish you need to duplicate this service (see IBM Cloud Pak for Multicloud Management documentation on how to duplicate a service) in the user assigned namespace and then publish it to service library.

* [Test Deploy the Service](#test-deploy-the-service)
* [Deploying the service from Service Library](#deploying-the-service-from-service-library)

### Prerequisites
- Navigate to Manage -> Shared Parameters -> In Search Data Type, Enter "vSphere Managed Inventory Definition" -> Verify Data Type is present
- Go to Create Data Object -> Select Data Type "vsphere_managed_inventory_definition" -> Enter Data Object Name for e.g. "vsphere_config". Fill the following paramaters.

| Parameter name                  | Type            | Parameter description      | Allowed values |
| :---                            | :---            | :---                       | :---           |
| datacenter                      | string      | The name of a datacenter in which to create the virtual machine and other assets.                                                | |
| resource_pool                   | string          | Name of the default resource pool for the cluster. Must be specified as 'cluster_name/resource_pool'                       | |
| vm_folder                       | string          | vSphere folder name to create the virtual vachine.                                                                         | |
| vm_image_template               | string          | Virtual machine image template name. If it is in a folder then include folder name as follows 'folder_name/image_template_name'                                                             | |
| vm_domain_name                  | string          | Virtual machine domain name.                                                                            | |
| vm_os_user                      | string          | The user name to connect to the virtual machine                                                                          | |
| vm_os_private_ssh_key           | string          | The user private key to connect to the virtual machine.                                                                         | |
| vm_os_public_ssh_key            | string          | Virtual Machine Template User Public Key to be added to the VM                                                                  | |
| vm_os_password                  | string          | The user password to connect to the virtual machine.                                                                         | |
| datastore                       | string          | Virtual machine datastore nam                                                                              | |
| network                         | string          | vSphere Network name.                                                                            | |
| adapter_type                    | string          | Network adapter type for vNIC Configuration                                                                    | |
| dns_servers                     | list          | A list of DNS servers to add on the virtual machine.                                                                         | |
| dns_suffixes                    | list          | A list of DNS search domains to add to the DNS configuration on the virtual machine.                                            | |
| vm_ipv4_gateway                 | string          | IPv4 Gateway Address for network customization on the virtual machine.                                                          | |
| vm_ipv4_netmask                 | string          | Integer value between 1 and 32 for the prefix length (CIDR) to use when statically assigning an IPv4 address                   | |
| vm_clone_timeout                | string          | The timeout, in minutes, to wait for the virtual machine clone to complete.                                                                        | |

## Test Deploy the Service

To deploy this service from IBM Cloud Automation Manager navigate to Automate Infrastructure > Manage Services  > Virtual Machine > Virtual Machine on VMware. Fill the following input parameters and deploy the service.

| Parameter name             | Type            | Parameter description      | Allowed values |
| :---                       | :---            | :---                       | :---           |
| Connection                 | connection      | VMware Vsphere connection                                                                                    | |
| vm_name                    | string          | Hostname of virtual machine                  | |
| vm_ipv4_address            | string          | IPv4 address for vNIC configuration          | |
| vSphere Managed Inventory Definition                 | sharedparameter      | Data object of type "vsphere_managed_inventory_definition" | |
| VM Memory Allocation (MB)                 | string      |  | |
| VM vCPU Allocation                | string      |  | |
| vm_disk_size                 | string      |  | |

## Deploying the service from Service Library

To deploy this service from Service Library navigate to Automate Infrastructure > Service Library, select the published service and fill the following input parameters and install the service.

| Parameter name             | Type            | Parameter description      | Allowed values |
| :---                       | :---            | :---                       | :---           |
| Connection                 | connection      | VMware Vsphere connection                                                                                    | |
| vm_name                    | string          | Hostname of virtual machine                  | |
| vm_ipv4_address            | string          | IPv4 address for vNIC configuration          | |
| vSphere Managed Inventory Definition                 | sharedparameter      | Data object of type "vsphere_managed_inventory_definition" | |
| VM Memory Allocation (MB)                 | string      |  | |
| VM vCPU Allocation                | string      |  | |
| vm_disk_size                 | string      |  | |


### License and Maintainer

Copyright IBM Corp. 2020

Service Version - 1.0.0.0
 