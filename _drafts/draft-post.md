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
Sort-Object -Property VMHost | Format-Table -AutoSize
```

### Explanation
I have chosen just one datastore in [Get-DataStore](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Get-Datastore.html). Multiple  datastores can be chosen via a couple of methods. I like to use [Regular Expressions](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_regular_expressions?view=powershell-6) or all datastores presented to an ESX Host. All datastores will be displayed along with their multipathing information. These objects are [piped](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_pipelines?view=powershell-6) to [Get-ScsiLun](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Get-ScsiLun.html) which are then *piped* to [Select-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-6).

Using *Select-Object*, I'm displaying the VMHost and CanonicalName property values from *Get-ScsiLun*. The script also uses a [Calculated Property](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-6#examples) which is named *SAN ID*. This could be named anything, I have chosen to give it the same name as the property I'm retrieving the value for from [Get-ScsiLunPath](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Get-ScsiLunPath.html)

*@{Name='SAN ID';Expression={($_ | Get-ScsiLunPath).SanID }}*

Using the [Automatic Variable](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_automatic_variables?view=powershell-6) *$_* I'm using the current object in the pipeline, in this case, *Get-ScsciLun* and piping it to *Get-ScsiLunPath*. Using brackets/parentheses the SanID property is chosen.

*($_ | Get-ScsiLunPath).SanID*

This propery is the value of the vmhba path to the specified SCSI device.

[Sort-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/sort-object?view=powershell-6) has been added in if you are checking multiple VMware hosts. 

*Sort-Object - Property VMHost* will keep all of the VMware hosts together and sorted by name. 

Finally, [Format-Table](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/format-table?view=powershell-6) is used to output the information as a table.

*Format-Table -AutoSize* adjusts the column size and number of columns based on the width of the data.


### Results
I edited the results below to easily show the CanonicalName and SAN ID. The first results display when only 1 path is visible from VMware to the storage. The second results show when 4 paths are visible.
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

The above script can be very useful to confirm that your VMware ESXi environment is able to see all of the paths that are presented. If  paths are missing, you can then troubleshoot your environment for any misconfigurations. 

Hope you're having a great day and this is of use.

Thanks, Tim.
