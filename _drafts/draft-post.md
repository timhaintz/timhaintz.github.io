---
layout: post
title: "Template Title"
date: 2018-08-04
---
## Machine Uptime
There was a question on StackExchange/SuperUser, [How to know how long I have launched this machine](https://superuser.com/questions/1255236/how-to-know-how-long-i-have-launched-this-machine/1255476#1255476), asking the equivalent of *uptime* in Linux. Please see my below answer using PowerShell.

### Script
#### PowerShell Code Block
#### Machine Name and Uptime
```PowerShell
Get-CimInstance -ClassName win32_operatingsystem | Select-Object csname, @{name="Uptime"; expression = {((Get-Date)-($_.lastbootuptime))}}

csname Uptime             
------ ------             
ca1    12.23:50:46.6914567
```

#### Uptime - Days to TotalMilliseconds
```PowerShell
New-TimeSpan -start (Get-CimInstance -ClassName win32_operatingsystem).LastBootUpTime -end (Get-Date)

Days              : 12
Hours             : 23
Minutes           : 52
Seconds           : 35
Milliseconds      : 887
Ticks             : 11227558871585
TotalDays         : 12.9948598050752
TotalHours        : 311.876635321806
TotalMinutes      : 18712.5981193083
TotalSeconds      : 1122755.8871585
TotalMilliseconds : 1122755887.1585
```

#### Uptime - Days, Hours and Minutes
```PowerShell
New-TimeSpan -start (Get-CimInstance -ClassName win32_operatingsystem).LastBootUpTime -end (Get-Date) | Select-Object Days,Hours,Minutes

Days Hours Minutes
---- ----- -------
  12    23      53

```


### Explanation

### *[Get-CimInstance](https://docs.microsoft.com/en-us/powershell/module/cimcmdlets/get-ciminstance?view=powershell-6)*

### *-ClassName*

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
