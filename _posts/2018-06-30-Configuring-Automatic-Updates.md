---
layout: default
title: "Configuring Automatic Updates - Group Policy or Registry"
date: 2018-06-30
---
# {{ page.title }}

## Introduction

If Automatic Updates are managed by [Group Policy](https://msdn.microsoft.com/en-us/library/ee663280(v=vs.85).aspx) or via the [Registry](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724871(v=vs.85).aspx), it is nice to be able to confirm that the Group Policy setting has applied correctly. The registry key required for Automatic Updates is located in *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU* as described in [this](https://support.microsoft.com/en-au/help/328010/how-to-configure-automatic-updates-by-using-group-policy-or-registry-s) Microsoft Support document. If [WSUS](https://docs.microsoft.com/en-us/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) is available, the registry key is located in *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate*. The values available to these registry keys are available in the [Configure Automatic Updates in a Non–Active Directory Environment](https://docs.microsoft.com/fr-fr/security-updates/windowsupdateservices/18127152) document.
*Please note, this link is a French language page. The values are in English. At the time of writing, the English page equivalent does not exist.*

### Script

#### PowerShell Code Block - WSUS and Automatic Update Registry Keys

```powershell
# Locations to check for Automatic Update settings
Get-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate
Get-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU

# Script to retrieve Automatic Update registry values from remote machines
$cred = Get-Credential
Invoke-Command -ComputerName (Get-ADComputer -Filter {name -like 'srv*'}).name -ScriptBlock {Get-ItemProperty HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU} -Credential $cred
```

### Explanation

[Get-ItemProperty](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-itemproperty?view=powershell-6) in this instance retrieves the registry entries and their values. By default, HKLM: is mapped as a PowerShell drive to the *HKEY_LOCAL_MACHINE* hive of the registry.

[Invoke-Command](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-6) is used and the -ComputerName paramater uses the [Get-ADComputer](https://technet.microsoft.com/es-es/library/hh852328(v=wps.630).aspx) cmdlet to retrieve the required servers.
*Please see this [blog post](https://github.com/timhaintz/timhaintz.github.io/blob/master/_posts/2018-05-04-PowerShell-Get-ADComputer.md) to install the Remote Server Administration Tools and gain access to the Get-ADComputer cmdlet.*

#### *-ComputerName*

To retrive the names of the servers, I'm using *(Get-ADComputer -Filter {name -like 'srv*'}).name* as the value for the -ComputerName paramater. This checks active directory for any machines with a name like *srv*. The * is for a wildcard search.

#### *-ScriptBlock*

Running *Get-ItemProperty HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU* as the ScriptBlock paramater runs the command on the remote machine.

#### *-Credential*

[Get-Credential](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential?view=powershell-6) stores the appropriate username and password in the *$cred* variable.

#### PowerShell Code Block - Setting the $cred variable

```powershell
$cred = Get-Credential
```

The results of the script is shown below.

### Results

```powershell
AUOptions                 : 3
DetectionFrequency        : 20
DetectionFrequencyEnabled : 1
PSPath                    : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU
PSParentPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate
PSChildName               : AU
PSDrive                   : HKLM
PSProvider                : Microsoft.PowerShell.Core\Registry
PSComputerName            : Srv1
RunspaceId                : dff61f57-2a4e-4767-9f5f-72af18d52313

AUOptions      : 3
PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate
PSChildName    : AU
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PSComputerName : Srv2
RunspaceId     : 6e5c234b-075d-42d1-a65b-238c43aa3e56
```

The above results show *Srv1* has *AUOptions*,*DetectionFrequency* and *DetectionFrequencyEnabled* set. *Srv2* only has *AUOptions* set. If a setting isn't as it seems, you can modify it and then run the script again to conifrm that all server settings are compliant.

### Conclusion

Using *Invoke-Command* as above is a quick method to iterate through and view multiple remote machine details quickly. The *ScriptBlock* and *Credential* paramaters allow it to run remote commands in an authenticated manner.

Hope you're having a great day and this is of use.

Thanks, Tim.
