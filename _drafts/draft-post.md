---
layout: post
title: "Hyper-V Heartbeat"
date: 2018-12-24
---
# {{ page.title }}

## Introduction

### Script

#### PowerShell Code Block

```PowerShell
# Wait for Hyper-V heartbeat
Start-Sleep -seconds 20
Remove-PSSession -Session $session
# Wait for the VM's heartbeat integration component to come up if it is enabled
$heartbeatic  = (Get-VM | where {$_.Name -eq "$vmname"} | `
                 Get-VMIntegrationService)
If ($heartbeatic -and ($heartbeatic.Enabled -eq $true))
{
    $startTime = Get-Date
    do
    {
        $timeElapsed = $(Get-Date) - $startTime
        if ($($timeElapsed).TotalMinutes -ge 2)
        {
            Write-Host "Heartbeat Integration Components did not come up after 2 minutes" `
                        -MessageType Error
            throw
        }
        Start-Sleep -sec 1
    }
    until ($heartbeatic.PrimaryStatusDescription -eq "OK")
    Write-Host "$vmname has successfully rebooted. Hyper-V has received a heartbeat from $vmname. Please wait." -ForegroundColor Green
$session = New-PSSession -VMName $vmname -Credential $domaincred
}

```

### Results

```PowerShell

```

## Explanation

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
![HTML Report](/assets/20180531/HTML-EmailAsFile.png)

## Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
