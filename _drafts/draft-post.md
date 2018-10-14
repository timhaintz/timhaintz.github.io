---
layout: post
title: "Template Title"
date: 2018-08-30
---

### Introduction

### Script
#### PowerShell Code Block
```PowerShell
((Get-ADUser azureadmin -Properties PasswordLastSet).passwordlastset).adddays(30)
```

### Results
```PowerShell
((Get-ADUser azureadmin -Properties PasswordLastSet).passwordlastset).adddays(30)

Monday, November 12, 2018 9:39:35 PM
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
