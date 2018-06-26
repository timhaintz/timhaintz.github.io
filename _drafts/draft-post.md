---
layout: post
title: "Automatic Updates"
date: 2018-06-14
---
## Configuring Automatic Updates - Group Policy or Registry
If Automatic Updates are managed by [Group Policy](https://msdn.microsoft.com/en-us/library/ee663280(v=vs.85).aspx) or via the [Registry](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724871(v=vs.85).aspx), it is nice to be able to confirm that the Group Policy setting has applied correctly. The registry key required for Automatic Updates is located in *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU* as described in [this](https://support.microsoft.com/en-au/help/328010/how-to-configure-automatic-updates-by-using-group-policy-or-registry-s) Microsoft Support document. If [WSUS](https://docs.microsoft.com/en-us/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) is available, the registry key is located in *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate*. The values available to these registry keys are available in the [Configure Automatic Updates in a Non–Active Directory Environment](https://docs.microsoft.com/fr-fr/security-updates/windowsupdateservices/18127152) document. 
*Please note, this link is a French language page. The values are in English. At the time of writing, the English page equivalent does not exist.*

### PowerShell Code Block - WSUS and Automatic Update Registry Keys
```PowerShell
# Locations to check for Automatic Update settings
Get-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate
Get-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU

# Script to retrieve Automatic Update registry values from remote machines
$cred = Get-Credential
Invoke-Command -ComputerName (Get-ADComputer -Filter {name -like 'srv*'}).name -ScriptBlock {Get-ItemProperty HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU} -Credential $cred

```

### Explanation
Using [Get-ItemProperty](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-itemproperty?view=powershell-6), you can retrieve the registry entries and their values. By default, HKLM: is mapped as a PowerShell drive to the *HKEY_LOCAL_MACHINE* hive of the registry. 

[Get-Credential](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential?view=powershell-6) stores the appropriate username and password in the *$cred* variable.

[Invoke-Command](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-6) is used and the -ComputerName paramater uses the [Get-ADComputer](https://technet.microsoft.com/es-es/library/hh852328(v=wps.630).aspx) cmdlet to retrieve the required servers.
*Please see this [blog post](https://github.com/timhaintz/timhaintz.github.io/blob/master/_posts/2018-05-04-PowerShell-Get-ADComputer.md) to install the Remote Server Administration Tools and gain access to the Get-ADComputer cmdlet.*


### Results
```PowerShell
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

### Insert Assets
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})


Hope you're having a great day and this is of use.

Thanks, Tim.
