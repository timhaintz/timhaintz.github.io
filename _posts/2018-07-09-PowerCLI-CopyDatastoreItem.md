---
layout: post
title: "PowerCLI - Copy-DatastoreItem"
date: 2018-07-09
---
## PowerCLI - Copy-DatastoreItem
[Copy-DatastoreItem](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Copy-DatastoreItem.html) copies items/files between datastores and between a datastore and a local file system provider.

### Script
#### PowerShell Code Block
```PowerShell
# PowerCLI VMware copy datastore to datastore
Copy-DatastoreItem -Item 'vmstores:\virtualcentername@443\SAS7K_ISOs\RHEL-7\' -Destination 'vmstores:\virtualcentername@443\SSD_ISOs\' -Recurse

# PowerCLI VMware copy local file to vCenter datastore
Copy-DatastoreItem -Item 'c:\ISOs\' -Destination 'vmstores:\virtualcentername@443\SSD_ISOs\' -Recurse
```

### Explanation

#### *[Copy-DatastoreItem](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Copy-DatastoreItem.html)*
[Copy-DatastoreItem](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Copy-DatastoreItem.html) can be used to copy between vCenters, if you are connected to two vCenters in PowerCLI, between datastores in the same vCenter and also from a local system provider to a vCenter.

#### *-Item*
This is the source file or folder. The *RHEL-7* folder is the source folder.

#### *-Destination*
This is the destination file or folder. Please note that the path ends with *\*. *SSD_ISOs* is the destination folder. *RHEL-7* will be copied to *SSD_ISOs*.

#### *-Recurse*
Copy the item as well as its children items.


### Conclusion
The above is an automatable way to copy files and folders using PowerCLI without using the vSphere Web Client. You may use it to upload an ISO automatically once it has been created.

Hope you're having a great day and this is of use.

Thanks, Tim.
