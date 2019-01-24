---
layout: default
title: "Password Expiry Date"
date: 2018-10-14
---
# {{ page.title }}

## Introduction

Below is a one liner to advise when a user password will expire. I have used the Group Policy default setting of 42 days in the example below. The [Maximum Password Age](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-password-age) link has further information on the Group Policy setting.

### Script

#### PowerShell Code Block

```powershell
((Get-ADUser -Identity azureadmin -Properties PasswordLastSet).passwordlastset).adddays(42)
```

### Results

```powershell
((Get-ADUser -Identity azureadmin -Properties PasswordLastSet).passwordlastset).adddays(42)

Saturday, November 24, 2018 9:39:35 PM
```

## Explanation

### Cmdlets used

### *[Get-ADUser](https://docs.microsoft.com/en-us/powershell/module/addsadministration/get-aduser?view=win10-ps)*

The *Get-ADUser* cmdlet gets a specified user object or performs a search to get multiple user objects.

### *-Identity*

Specifies an Active Directory user object.

### *-Properties*

Specifies the properties of the output object to retrieve from the server. Use this parameter to retrieve properties that are not included in the default set.

### *[adddays() method](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.adddays?view=netframework-4.7.2)*

By using parentheses around *(Get-ADUser -Identity azureadmin -Properties PasswordLastSet).passwordlastset)* I can call the [adddays()](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.adddays?view=netframework-4.7.2) method. Scripting Guy has a great blog post called [Adding and Subtracting Dates with PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/01/21/adding-and-subtracting-dates-with-powershell/) if you would like further backgound. Using adddays() allows me to take a DateTime object and add days or, using a -, subtract days.

## Conclusion

The above one liner is a quick and easy way to check when a user password will expire. It also shows how PowerShell can be used to view and manipulate date time objects.

Hope you're having a great day and this is of use.

Thanks, Tim.
