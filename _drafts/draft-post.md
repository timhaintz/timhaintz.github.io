---
layout: default
title: "How many test users would you like?"
date: 2019-05-22
---
# {{ page.title }}

## Introduction

When testing, it is usefull to be able to create and destroy users repeatedly. A straight forward method I use to create multiple users is using the PowerShell [Range operator ..](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-6#range-operator-). This allows me to pipe a range of numbers (if you're using PowerShell 6, the range operator also works with *Characters*) into the `ForEach-Object` cmdlet.

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

####

```powershell
Get-ADUser -Filter * -SearchBase 'OU=Employees,DC=timhaintz,DC=com' | Remove-ADUser -Confirm:$false
```

## Explanation

This method can be used to create many users very quickly. Change the range of numbers and it will create that many users. For example, `1..10000` will create 10,000 users.

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

![Name of Image](/assets/20180531/HTML-EmailAsFile.png)

## Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
