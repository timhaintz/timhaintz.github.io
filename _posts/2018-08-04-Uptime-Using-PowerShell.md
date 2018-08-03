---
layout: post
title: "Uptime Using PowerShell"
date: 2018-08-04
---
### Introduction
There was a question on StackExchange/SuperUser, [How to know how long I have launched this machine](https://superuser.com/questions/1255236/how-to-know-how-long-i-have-launched-this-machine/1255476#1255476), asking the equivalent of *uptime* in Linux. Please see my answer below using PowerShell.

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
New-TimeSpan -start (Get-CimInstance -ClassName win32_operatingsystem).LastBootUpTime -end (Get-Date) | Select-Object -Property Days,Hours,Minutes

Days Hours Minutes
---- ----- -------
  12    23      53

```


### Explanation
The above code blocks display multiple ways of retrieving the uptime of a machine. Using [Get-CimInstance](https://docs.microsoft.com/en-us/powershell/module/cimcmdlets/get-ciminstance?view=powershell-6) and querying the [win32_operatingsystem](https://docs.microsoft.com/en-us/windows/desktop/cimwin32prov/win32-operatingsystem) WMI class for the LastBootUpTime value enables a simple calculation of the time right now *Get-Date* minus LastBootUpTime. The calculation is being performed in a [Select-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-6) calculated propery. The first example could be added into a [ForEach Statement](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_foreach?view=powershell-6) to iterate through multiple machines. The name of the machine and uptime are displayed together.

[New-TimeSpan](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/new-timespan?view=powershell-6) creates a TimeSpan object can be used to add or subtract time from DateTime objects.
Using *New-TimeSPan* with a *-Start* and *-End* Parameter, the *LastBootUpTime* and current time *Get-Date* are compared and the difference returned.

In the final code block, [Select-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-6) is being used to retrieve only the desired properties.



### Cmdlets used
### *[Get-CimInstance](https://docs.microsoft.com/en-us/powershell/module/cimcmdlets/get-ciminstance?view=powershell-6)*
Gets the CIM instances of a class from a CIM server.

### *-ClassName*
Specifies the name of the CIM class for which to retrieve the CIM instances. NOTE: You can use tab completion to browse the list of classes, because PowerShell gets a list of classes from the local WMI server to provide a list of class names.

### *[Select-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-6)*
Selects specific properties of an object or set of objects.

### *-Property*
Specifies the properties to select.

### *[New-TimeSpan](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/new-timespan?view=powershell-6)*
The New-TimeSpan cmdlet creates a TimeSpan object that represents a time interval. You can use a TimeSpan object to add or subtract time from DateTime objects.

### *-Start*
Specified the start of a time span. Enter a string that represents the date and time or a DateTime object.

### *-End*
Specifies the end of a time span.

### Conclusion
Being able to run a 'one liner' to determine the uptime a machine saves a lot of time. You don't have to login to the machine and check event logs or the *Ethernet Status*. You could also run it remotely if you have [PowerShell Remoting](https://docs.microsoft.com/en-us/powershell/scripting/core-powershell/running-remote-commands?view=powershell-6) setup.

Hope you're having a great day and this is of use.

Thanks, Tim.
