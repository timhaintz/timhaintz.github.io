---
layout: post
title: "Ping -t - The PowerShell Way"
date: 2018-06-04
---
## Ping -t - The PowerShell Way

```PowerShell
$add5Mins = (Get-Date).AddMinutes(5)

while ((Get-Date) -le $add5Mins)
{
    "$(Get-Date);$(Test-Connection -Count 1  -ComputerName srv1 -Quiet)";Start-Sleep -Seconds 20
}
```

Rebooting srv1
```PowerShell
PS C:\Windows\system32> $add5Mins = (Get-Date).AddMinutes(5)

while ((Get-Date) -le $add5Mins)
{
    "$(Get-Date);$(Test-Connection -Count 1  -ComputerName srv1 -Quiet)";Start-Sleep -Seconds 20
}
06/03/2018 18:39:35;True
06/03/2018 18:39:55;True
06/03/2018 18:40:15;True
06/03/2018 18:40:35;False
06/03/2018 18:40:59;False
06/03/2018 18:41:23;True
06/03/2018 18:41:43;True
06/03/2018 18:42:03;True
06/03/2018 18:42:23;True
06/03/2018 18:42:43;False
06/03/2018 18:43:07;True
06/03/2018 18:43:27;True
06/03/2018 18:43:47;True
06/03/2018 18:44:07;True
06/03/2018 18:44:27;True

PS C:\Windows\system32> 
```

Hope you're having a great day and this is of use.

Thanks, Tim.
