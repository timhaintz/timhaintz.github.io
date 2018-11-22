---
layout: post
title: "My First Pester Test"

date: 2018-11-14
---
### Introduction
I first read [The Pester Book](https://leanpub.com/pesterbook) a couple of years ago. Below is my first Pester test. It tests if the *Guest* user account is enabled in Active Directory.

I used [Write Your First Pester Test Today](https://sqldbawithabeard.com/2017/11/16/write-your-first-pester-test-today/) as a guide.

I plan on writing a lot more Pester Tests and discussing them here.

### Script
#### PowerShell Code Block
```powershell
Describe "Testing Guest Account Disabled" {
    Context "Logins" {
        It "The Guest account should be disabled"{
            (Get-ADUser Guest).Enabled | Should be 'False'
        }
    }
}
```
Save the above code block with a *.Tests.ps1* extension. For this example, I have saved the file as *ActiveDirectory.Tests.ps1*

### Results
```powershell
Set-ADUser guest -Enabled $true

Invoke-Pester C:\Users\azureadmin\ActiveDirectory.Tests.ps1

Describing Testing Guest Account Disabled
   Context Logins
    [-] The Guest account should be disabled 46ms
      Expected: {False}
      But was:  {True}
      4:             (Get-ADUser Guest).Enabled | Should be 'False'
      at <ScriptBlock>, C:\Users\azureadmin\ActiveDirectory.Tests.ps1: line 4
Tests completed in 46ms
Passed: 0 Failed: 1 Skipped: 0 Pending: 0 Inconclusive: 0

Set-ADUser guest -Enabled $false

Invoke-Pester C:\Users\azureadmin\ActiveDirectory.Tests.ps1

Describing Testing Guest Account Disabled
   Context Logins
    [+] The Guest account should be disabled 40ms
Tests completed in 40ms
Passed: 1 Failed: 0 Skipped: 0 Pending: 0 Inconclusive: 0

```

![Pester Test Results]({{ "/assets/20181114/1-PesterTest.png" | absolute_url }})

### Conclusion
This post was written as my first attempt at a Pester Test, using Active Directory. Hopefully you can think of some uses in your own environment to start running Pester Tests. I look forward to writing more about Pester and learning more about [Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development).

Hope you're having a great day and this is of use.

Thanks, Tim.
