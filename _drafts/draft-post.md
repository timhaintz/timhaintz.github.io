---
layout: default
title: "Pester - Testing multiple services on a remote server"
date: 2019-02-04
---
# {{ page.title }}

## Introduction

I've been looking into utilising Pester for infrastructure auditing. This was driven through my use of [InSpec](https://www.inspec.io/), Chef's Audit and Testing Framework. I like the idea of Pester as it is already 'built in' to the operating system (Windows 10 and Server 2016).

Something useful to check is if specific services are running on a remote machine.

The below Pester test checks for a number of services and returns if they're running or not.

### Script

#### PowerShell Code Block

```powershell
# Thanks to: https://sqldbawithabeard.com/2017/11/28/2-ways-to-loop-through-collections-in-pester/
# Services we want to test for
$services = 'bthserv','WinRM'
# Loop through the services
Describe "Testing critical services on ca1" {
    $services.ForEach{
        Context "Testing $($_)" {
            It "The $($_) service should be running" {
                (Invoke-Command -ComputerName ca1 -ScriptBlock {param($_) Get-Service -ServiceName $_} -Credential $cred -ArgumentList $_ ).status | Should be 'Running'
            }
        }
    }
}

```

### Results

When a service is off, the below failure is displayed.
![Pester Multiple Services - Remote Fail](/assets/20180531/HTML-EmailAsFile.png)

When the services are all running, the below success is displayed.
![Pester Multiple Services - Remote Pass](/assets/20180531/HTML-EmailAsFile.png)

## Explanation

You can add the services you choose to be tested. This will loop through as many services as you chooose.
You could also add another loop around this one to change the server name. You could then check multiple servers for the services.

## Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
