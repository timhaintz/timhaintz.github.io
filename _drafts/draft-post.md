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

#### *Cmdlet 1*

#### *-Paramater 1*

#### *-Paramater 2*

#### *-Paramater N*

#### *Cmdlet N*

#### *-Paramater 1*

#### *-Paramater 2*

#### *-Paramater N*

### Results
```PowerShell

```

### Insert Assets
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})

### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
