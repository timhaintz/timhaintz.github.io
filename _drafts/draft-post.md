---
layout: default
title: "How many test users would you like?"
date: 2019-05-22
---
# {{ page.title }}

## Introduction

When testing, it is usefull to be able to create and destroy users repeatedly. A straight forward method I use to create multiple users is using the PowerShell [Range operator ..](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-6#range-operator-). This allows me to pipe a range of numbers (if you're using PowerShell 6, the range operator also works with *Characters*) into the [ForEach-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/foreach-object?view=powershell-6)cmdlet.

### Script

#### Range operator PowerShell Code Block

Range operator in use:

```powershell
1..4
```

Displays and outputs:

```powershell
1
2
3
4
```

#### New-ADUser PowerShell Code Block

```powershell
New-ADOrganizationalUnit -Name "Employees" -Path "DC=TIMHAINTZ,DC=COM"

1..10 | ForEach-Object {New-ADUser -Name "User-$_" -samAccountname "User-$_" -UserPrincipalName "User-$_`@timhaintz.com" -Path "OU=Employees,DC=timhaintz,DC=com" -enabled $true -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -force)}

```

## Results

![Name of Image](/assets/20180531/HTML-EmailAsFile.png)

```powershell
Get-ADUser user-4


DistinguishedName : CN=User-4,OU=Employees,DC=timhaintz,DC=com
Enabled           : True
GivenName         :
Name              : User-4
ObjectClass       : user
ObjectGUID        : 20106c20-3083-4ad5-ae13-2af862b999f1
SamAccountName    : User-4
SID               : S-1-5-21-1031186934-257834335-2802136171-1106
Surname           :
UserPrincipalName : User-4@timhaintz.com
```

To delete all of the users in the Organizational Unit without prompting for confirmation, run the below.

### Delete users PowerShell Code Block

```powershell
Get-ADUser -Filter * -SearchBase 'OU=Employees,DC=timhaintz,DC=com' | Remove-ADUser -Confirm:$false
```

## Explanation

This method can be used to create many users very quickly. Changing the range of numbers will create that many users. For example, `1..10000` will create 10,000 users. Combining the range operator and Active Directory cmdlets, you can quickly deploy test solutions for your needs.

### PowerShell tools used

### *[Range operator ..](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-6#range-operator-)*

From the documentation, "Represents the sequential integers in an integer array, given an upper, and lower boundary."
*From PowerShell 6, the range operator works with Characters as well as Integers.*

### *[ForEach-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/foreach-object?view=powershell-6)*

Performs an operation on each item in a collection. We piped the output from the range operator into ForEach-Object.

### *[New-ADOrganizationalUnit](https://docs.microsoft.com/en-us/powershell/module/addsadministration/new-adorganizationalunit?view=win10-ps)*

Create an Active Directory Organizational Unit.

### *-Name*

Specifies the name of the object.

### *-Path*

Specifies the X.500 path of the OU or container where the object is created. See *-path* under [Optional Parameters](https://docs.microsoft.com/en-us/powershell/module/addsadministration/new-adorganizationalunit?view=win10-ps#optional-parameters) for further details.

### Insert Assets

![Name of Image](/assets/20180531/HTML-EmailAsFile.png)

## Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
