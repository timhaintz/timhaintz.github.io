---
layout: post
title: "Windows Update - WSUS"
date: 2018-06-14
---
## Windows Update Settings - Group Policy or Registry
If Windows Update is managed by Group Policy, it is good to be able to confirm that the Group Policy setting is applied correctly.

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
