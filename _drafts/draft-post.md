---
layout: default
title: "Pester - Testing multiple services on a remote server"
date: 2019-01-28
---
# {{ page.title }}

## Introduction
Something I've been looking into for Pester is Infrastructure auditing. Is something the way you expect it. I'm also looking to do this to remove machines. Something useful is to check if certain services are running on a remote machine.

The below Pester test checks for a number of services and returns if they're running or not.

### Script

#### PowerShell Code Block

```PowerShell
# Thanks to: https://sqldbawithabeard.com/2017/11/28/2-ways-to-loop-through-collections-in-pester/
$cred = Get-Credential azureadmin
# Services we want to test for
$services = 'Service1','Service2'
# Fill the testCases with the values and name of the Service
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

```PowerShell

```

## Explanation


### Insert Assets
![HTML Report](/assets/20180531/HTML-EmailAsFile.png)

## Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
