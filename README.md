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

First, [download a pre-built Packer
binary](https://www.packer.io/downloads.html) for your operating system or
[compile Packer
yourself](https://github.com/hashicorp/packer/blob/master/.github/CONTRIBUTING.md#setting-up-go-to-work-on-packer).


