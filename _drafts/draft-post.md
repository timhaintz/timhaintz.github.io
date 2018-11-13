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

### Results
```PowerShell

```

### Explanation


### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
