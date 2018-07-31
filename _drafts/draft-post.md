---
layout: post
title: "Template Title"
date: 2018-08-04
---
## Machine Uptime
There was a question on StackExchange asking the equivalent of *uptime* in Linux. Please see below.

### Script
#### PowerShell Code Block
```PowerShell
# Check how long a machine has been up for
Get-CimInstance -ClassName win32_operatingsystem | select csname, @{name="Uptime"; expression = {((get-date)-($_.lastbootuptime))}}
New-TimeSpan -start (Get-CimInstance -ClassName win32_operatingsystem).LastBootUpTime -end (get-date) 
New-TimeSpan -Start ((Get-WmiObject win32_operatingsystem | Select-Object @{Name='LastBootUptime';Expression={$_.ConverttoDateTime($_.lastbootuptime)}}).lastbootuptime) -End (get-date) 
```

### Results
```PowerShell

```

### Explanation

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
