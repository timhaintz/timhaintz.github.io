---
layout: post
title: "Automatic Updates"
date: 2018-06-14
---
## Configuring Automatic Updates - Group Policy or Registry
If Automatic Updates are managed by [Group Policy](https://msdn.microsoft.com/en-us/library/ee663280(v=vs.85).aspx) or via the [Registry](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724871(v=vs.85).aspx), it is nice to be able to confirm that the Group Policy setting has applied correctly. The registry key required for Automatic Updates is located in *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU* as described in [this](https://support.microsoft.com/en-au/help/328010/how-to-configure-automatic-updates-by-using-group-policy-or-registry-s) Microsoft Support document. If [WSUS]
(https://docs.microsoft.com/en-us/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) is available, the registry key is located in *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate*. The values available to these registry keys is available in the [Configure Automatic Updates in a Non–Active Directory Environment](https://docs.microsoft.com/fr-fr/security-updates/windowsupdateservices/18127152). 
*Please note, this link is a French language page. The values are in English. At the time of writing, the English page equivalent does not exist.*




### PowerShell Code Block - WSUS and Automatic Update Registry Keys
```PowerShell
Get-ItemProperty HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate
Get-ItemProperty HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU


$cred = Get-Credential
Invoke-Command -ComputerName (Get-ADComputer -Filter {name -like 'srv*'}).name -ScriptBlock {Get-ItemProperty HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU} -Credential $cred

```

### Explanation

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
