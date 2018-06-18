---
layout: post
title: "Automatic Updates"
date: 2018-06-14
---
## Configuring Automatic Updates - Group Policy or Registry
If Automatic Updates is managed by Group Policy or via the Registry, it is nice to be able to confirm that the Group Policy setting is applied correctly. The registry key required for Automatic Updates is located at *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU* as described in [this](https://support.microsoft.com/en-au/help/328010/how-to-configure-automatic-updates-by-using-group-policy-or-registry-s) Microsoft Support document.

### PowerShell Code Block - Windows Update Registry Key
```PowerShell
Get-Item HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate
```

### Explanation

### Results
```PowerShell

```

### Insert Assets
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})


Hope you're having a great day and this is of use.

Thanks, Tim.
