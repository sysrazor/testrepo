# GlobalPayments Image Creator (Azure, Packer) #

* Website: https://
* Google Chat: 
* Mailing list: [Google Groups](https://groups.google.com)

The Global Payments Image creator creates base image templates for use in the public cloud 'Azure'. 
The image creator utilizes Hashicorp's Packer product to create Global Payments approved images from the Azure provided base VM templates.

Packer is a tool for building identical machine images for multiple platforms
from a single source configuration.



## Source Code Structure

```bash
├── files
│   ├── dhclient-enter-hooks                       <-- Description Here
│   ├── gpn_name_resolution_fqdn.sh                <-- Description Here
│   └── gpn_name_resolution_simple.sh              <-- Description Here
│   
├── scripts 
│   ├── add-disk.sh                                <-- Description Here
│   ├── copy_image_to_gallery.bash                 <-- Description Here
│   ├── create_mount_points.bash                   <-- Description Here
│   ├── create_users.bash                          <-- Description Here
│   ├── create_vm.sh                               <-- Description Here
│   ├── delete_vm.sh                               <-- Description Here
│   ├── generate_dns.bash                          <-- Description Here
│   ├── harden_os.bash                             <-- Description Here
│   ├── image_gallery.bash                         <-- Description Here
│   ├── install_packages.bash                      <-- Description Here
│   ├── install_puppet.bash                        <-- Description Here
│   ├── install_repos.bash                         <-- Description Here
│   └── patch_vm.bash                              <-- Description Here
│
├── centos73.json                                  <-- Description Here
├── Jenkinsfile                                    <-- Description Here
├── Jenkinsfile.TEST                               <-- Description Here
├── rhel7lvm.json                                  <-- Description Here
├── rhel7lvm.private.json


```

## Quick Start
**Note:** There is a great
[introduction and getting started guide](https://www.packer.io/intro)
for those with a bit more patience. Otherwise, the quick start below
will get you up and running quickly, at the sacrifice of not explaining some
key points.

* First, [download a pre-built Packer
binary](https://www.packer.io/downloads.html) for your operating system or
[compile Packer
yourself](https://github.com/hashicorp/packer/blob/master/.github/CONTRIBUTING.md#setting-up-go-to-work-on-packer).

* Install [GIT](https://git-scm.com/downloads) if you don't have it

After your workstation is setup; clone the repo.

**To clone the repository (CLI)**

```bash
$ git clone https://github.com/YOUR-REPOSITORY
```

### Configure variables in the `OS.json` file
``` bash
  "variables": {
      "location": "eastus",                               <-- The Azure location where to build the VM
      "compute_name":"rhel7-base-{{timestamp}}",          <-- The name of the template VM 
      "resource_group_name":"rsg-azusenad-sys-01",        <-- Resource group where to build the VM
      "vnet_resource_group_name":"rsg-azusenad-net-01",   <-- Virtual Network Resource Group where the vNet resides
      "vnet_name":"us-east-dev",                          <-- Virtual Network the VM to be built on
      "vnet_subnet_name":"us-east-dev-tier2",             <-- vNet Subnet to use an Ip address from
      "vm_size": "Standard_DS12_v2"                       <-- Azure VM size
  },

```
* Login Variables
``` bash
    "client_id": "",          <-- Azure SP account to perform API actions with
    "client_secret": "",      <-- Azure SP password
    "tenant_id": "",          <-- Azure Tenant ID
    "subscription_id": "",    <-- Azure Subscription ID
```

Before we take this template and build an image from it, let's validate the template by running packer validate example.json. This command checks the syntax as well as the configuration values to verify they look valid. The output should look similar to below, because the template should be valid. If there are any errors, this command will tell you.
``` bash
$ packer validate example.json
Template validated successfully.
```

Next, let's build the image from this template. With a properly validated template, it is time to build the image. This is done by calling `packer build` with the template file. 
``` bash
$ packer build example.json
```
<details>
           <summary>rhel7lvm.private.json Break Down</summary>
           <p><ul> 
                <li> <b>Builders:</b> Information and details of the VM to create. OS, compute sizing and network information
                <li> <b>Provisioners:</b> Custimozing the OS, Executing specified scripts from the scripts directory, copying files to the new VM and executing inline commands
  </ul>
  </p>
         </details>
