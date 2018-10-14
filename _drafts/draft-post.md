---
layout: post
title: "Template Title"
date: 2018-08-30
---

### Introduction
Below is a one liner to check when a user password will expire. I have used the Group Policy default setting of 42 days in the example below. [Maximum Password Age](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-password-age) has further information on the Group Policy setting.

### Script
#### PowerShell Code Block
```PowerShell
((Get-ADUser azureadmin -Properties PasswordLastSet).passwordlastset).adddays(42)
```

### Results
```PowerShell
((Get-ADUser azureadmin -Properties PasswordLastSet).passwordlastset).adddays(42)

Saturday, November 24, 2018 9:39:35 PM
```

### Explanation

### Cmdlets used
### *Cmdlet 1*

### *-Paramater 1*

### *-Paramater 2*

### *-Paramater N*

### *Cmdlet N*

### *-Paramater 1*

### *-Paramater 2*

### *-Paramater N*

### Insert Assets
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})

### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
