---
layout: post
title: "VMware PowerCLI - Multipathing"
date: 2018-06-04
---
## VMware PowerCLI - Multipathing

Often it is useful to see multipathing information from your VMware hosts. This could be for reduncancy confirmation or testing. You may be migrating and need to confirm that multipathing is correct. The below script will give you the information you need. 

### PowerCLI code block
```PowerShell
Get-Datastore esx11_local | Get-ScsiLun | 
Select-Object VMHost,CanonicalName,@{Name='SAN ID';Expression={($_ | Get-ScsiLunPath).SanID }} | 
Sort-Object VMHost | Format-Table -AutoSize
```

### Explanation
I have chosen just one datastore in [Get-DataStore](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Get-Datastore.html). Multiple  datastores can be chosen via a couple of methods. I like to use [Regular Expressions](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_regular_expressions?view=powershell-6) or via ESX Host. All datastores will be displayed along with their multipathing information. These objects are [piped](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_pipelines?view=powershell-6) to [Get-ScsiLun](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Get-ScsiLun.html) which are then piped to Select-Object.

### Results
I edited the results below to easily show the CanonicalName and SAN ID. 
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
