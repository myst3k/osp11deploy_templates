# Red Hat OSP11 Overcloud Trial Deploy Templates for lab in VMware running on a single Dell R710

**Setup**
* 1x Undercloud
* 1x Controller Node
* 1x Computer Node
* 1x Ceph Storage Node

**Specs**
Undercloud: 40GB drive, 4x vCpu, 8GB RAM, 2x nics, external and provisioning

Controller: 50GB drive, 4x vCpu, 8GB RAM, 6x nics, provisioning, storageIp, storageMgmt, internalApi, tenant, and external

Compute: 200GB drive, 8x vCpu, 16GB RAM, 4x nics, provisioning, storageIp, internalApi, tenant

Ceph: 50GB, 200GB, 1TB drives, 4x vCpu, 8GB RAM, 3x nics, provisioning, storageIp, storageMgmt

**Networking**
I have individual port groups for the names of each service type, provisioning, storageIp, storageMgmt, internalApi, tenant, and external. All but external is mapped to the same vSwitch. Running vyOS as the router for provisioning network, and the external network is directly connected to my home router through a separate vSwitch in VMware.

**Challenges**
* Learning to use fake_pxe and power the vmware images on and off at the correct times
* On PXE boot the interfaces would be correct, however they would all rename themselves during the overcloud deployment causing it to fail since it lost connectivity after the reboot. I solved this with the user of the interface-mapping.yaml file.
* Mapping the storage drives did not work since VMware drives give no serial, or information about the drive besides the size. I just had to cross my fingers and hope that the 50GB would be recognized as sda, 200GB as sdb, and 1TB as sdc.
