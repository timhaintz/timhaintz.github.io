---
layout: post
title: "My First Pester Test"

date: 2018-10-17
---
### Introduction
I first read [The Pester Book](https://leanpub.com/pesterbook) a couple of years ago. Below is my first Pester test. It tests if the *Guest* user account is enabled in Active Directory.

I used [Write Your First Pester Test Today](https://sqldbawithabeard.com/2017/11/16/write-your-first-pester-test-today/) as a guide.

I plan on writing a lot more Pester tests and discussing them here.

### Script
#### PowerShell Code Block
```PowerShell
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
```PowerShell
PS C:\Users\azureadmin> Set-ADUser guest -Enabled $true

PS C:\Users\azureadmin> Invoke-Pester C:\Users\azureadmin\ActiveDirectory.Tests.ps1

Describing Testing Guest Account Disabled
   Context Logins
    [-] The Guest account should be disabled 46ms
      Expected: {False}
      But was:  {True}
      4:             (Get-ADUser Guest).Enabled | Should be 'False'
      at <ScriptBlock>, C:\Users\azureadmin\ActiveDirectory.Tests.ps1: line 4
Tests completed in 46ms
Passed: 0 Failed: 1 Skipped: 0 Pending: 0 Inconclusive: 0

PS C:\Users\azureadmin> Set-ADUser guest -Enabled $false

PS C:\Users\azureadmin> Invoke-Pester C:\Users\azureadmin\ActiveDirectory.Tests.ps1





Describing Testing Guest Account Disabled
   Context Logins
    [+] The Guest account should be disabled 40ms
Tests completed in 40ms
Passed: 1 Failed: 0 Skipped: 0 Pending: 0 Inconclusive: 0

PS C:\Users\azureadmin> 

```

### Explanation


### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
