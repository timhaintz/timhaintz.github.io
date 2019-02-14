---
layout: default
title: "Ping -t - The PowerShell Way"
date: 2018-06-04
---
# {{ page.title }}

## Introduction

How often have you run [Ping](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/ping) or *ping -t*? How often have you run *ping -t* and found it still running 6 hours later? 2 days later?
I know it has happened to me more than once. I thought "wouldn't it be nice to be able to run it for a pre-determined length of time".

We were doing some upgrades recently and we needed to run *ping -t*. A colleague asked if it was possible to add the date and time of the ping to the query.

Below is the result of these questions using PowerShell. Adding a date/time for each request and also running it for a pre-determined length of time.

### While Statement - Condition

I'm using a [while statement](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_while?view=powershell-6) to continue running the *statement list* until the result of while is false.
Using the Get-Date method AddMinutes(), I am adding 5 minutes from the current Get-Date to the *$add5mins* variable. This variable is then used in the while loop.

*while ((Get-Date) -le $add5Mins)*  resolves true whilst Get-Date is *less than or equal* to *$add5mins*. See [about_Operators](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-6) and [about_Comparison_Operators](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-6) for further information.

### While Statement - Statement List

In the *statement list* of the while statement, the value of Get-Date is returned using $(Get-Date).
The result of [Test-Connection -Quiet](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/test-connection?view=powershell-6) is used to return the value of either true or false. The *-Count 1* parameter is used as a single 'ping' test. *-ComputerName* is the name of the machine you are attempting to 'ping'.
[Start-Sleep](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/start-sleep?view=powershell-6) is used so that the output below in the results section were of reasonable size. *Start-Sleep* suspends the while statement for 20 seconds each 'loop'.

### PowerShell Code Block

```powershell
$add5Mins = (Get-Date).AddMinutes(5)

while ((Get-Date) -le $add5Mins)
{
    "$(Get-Date);$(Test-Connection -Count 1  -ComputerName srv1 -Quiet)";Start-Sleep -Seconds 20
}
```

### Results

Test-Connection is successful(True) and fails(False) as below. *False* is shown when I rebooted srv1 as Test-Connection failed.

```powershell
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

### PowerShell Code Block - Continual Test-Connection

If you do want a continual ping, you can use:

```powershell
while($true)
{
    "$(Get-Date);$(Test-Connection -Count 1  -ComputerName srv1 -Quiet)"
}
```

You will have to CTRL+C out of this.

While statements are very useful for time based and also quantity based loops. You can set them up to run for a certain period of time as I have above, or for a certain number of loops.

Hope you're having a great day and this is of use.

Thanks, Tim.
