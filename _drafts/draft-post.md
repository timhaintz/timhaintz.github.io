---
layout: post
title: "VMware PowerCLI - Multipathing"
date: 2018-06-04
---
## VMware PowerCLI - Multipathing

### PowerCLI code block
```PowerShell
Get-Datastore esx11_local | Get-ScsiLun | 
Select-Object VMHost,CanonicalName,@{Name='SAN ID';Expression={($_ | Get-SCsiLunPath).SanID }} | 
Sort-Object VMHost | Format-Table -AutoSize
```

### Results
```PowerShell
# Code block run with 1 path visible
VMHost  CanonicalName   SAN ID
------  -------------   ------
esx11   naa.00a06       F4:05

# Code block run with 4 paths visible
VMHost  CanonicalName   SAN ID
------  -------------   ------
esx11   naa.00a06       {F4:25, F4:34, F4:05, F4:14}
```


Hope you're having a great day and this is of use.

Thanks, Tim.
