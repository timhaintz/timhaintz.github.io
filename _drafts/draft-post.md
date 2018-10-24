---
layout: post
title: "My First Pester Test"

date: 2018-10-17
---
### Introduction
I first read about Pester a couple of years ago. I have never quite found a requirement to implement it. Until now. Below is my first Pester test. It tests if the *Guest* user account is enabled in Active Directory.

I used [Write Your First Pester Test Today](https://sqldbawithabeard.com/2017/11/16/write-your-first-pester-test-today/) as a guide.

I plan on writing a lot more Pester tests and writing about them here.

### Script
#### PowerShell Code Block
```PowerShell
Describe "Testing Guest Account Disabled" {
    Context "Logins" {
        It "The Guest account should be disabled"{
            (Get-ADUser Guest).Enabled | Should be 'False'
        }
```

### Results
```PowerShell

```

### Explanation

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
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})

### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
