---
layout: post
title: "PowerCLI - Copy-DataStoreItem"
date: 2018-07-03
---
## PowerCLI - Copy-DataStoreItem
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

#### *Copy-DatastoreItem*
[Copy-DatastoreItem](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Copy-DatastoreItem.html) can be used to copy between vCenters, if you are connected to two vCenters in PowerCLI, between datastores in the same vCenter and also from a local system provider to a vCenter.

#### *-Item*

#### *-Destination*


### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
