---
layout: default
title: "How many 'test' users would you like?"
date: 2019-06-03
---
# {{ page.title }}

## Introduction

When testing, it is usefull to be able to create and destroy users repeatedly. A straight forward method I use to create multiple users is using the PowerShell [Range operator ..](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-6#range-operator-) . This allows me to pipe a range of numbers (if you're using PowerShell 6, the range operator also works with *Characters*) into the [ForEach-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/foreach-object?view=powershell-6) cmdlet.

## Script

### Range operator PowerShell Code Block

Using the Range operator:

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

### New-ADUser PowerShell Code Block

```powershell
New-ADOrganizationalUnit -Name "Employees" -Path "DC=TIMHAINTZ,DC=COM"

1..10 | ForEach-Object {New-ADUser -Name "User-$_" -SamAccountname "User-$_" -UserPrincipalName "User-$_`@timhaintz.com" -Path "OU=Employees,DC=timhaintz,DC=com" -Enabled $true -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force)}

```

The above code block creates 10 users in the OU=Employees,DC=timhaintz,DC=com OU.

## Results

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

To delete the users, you can use `Get-ADUser` and pipe the result to `Remove-ADUser`. I have used the *Employees OU* to retrieve all of the users and then remove them.

### PowerShell tools used

### *[Range operator ..](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-6#range-operator-)*

From the documentation, "Represents the sequential integers in an integer array, given an upper, and lower boundary."
*From PowerShell 6, the range operator works with Characters as well as Integers.*

### *[New-ADOrganizationalUnit](https://docs.microsoft.com/en-us/powershell/module/addsadministration/new-adorganizationalunit?view=win10-ps)*

Create an Active Directory Organizational Unit.

### *-Name*

Specifies the name of the object.

### *-Path*

Specifies the X.500 path of the OU or container where the object is created. See *-path* under [Optional Parameters](https://docs.microsoft.com/en-us/powershell/module/addsadministration/new-adorganizationalunit?view=win10-ps#optional-parameters) for further details.

### *[ForEach-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/foreach-object?view=powershell-6)*

Performs an operation on each item in a collection. We piped the output from the range operator into ForEach-Object.

### *[New-ADUser](https://docs.microsoft.com/en-us/powershell/module/addsadministration/new-aduser?view=win10-ps)*

Creates a new user in Active Directory.

### *-Name*

Specifies the name of the object.

### *-SamAccountName*

Specifies the Security Account Manager [SAM](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc756748(v=ws.10)) name of the user.

### *-UserPrincipalName*

Specifies the User Principal Name [UPN](https://docs.microsoft.com/en-us/windows/desktop/adschema/a-userprincipalname) of the user.

### *-Path*

Specifies the X.500 path of the OU or container where the new object is created.

### *-Enabled*

Specifies if an account is enabled. An enabled account requires a password.

### *-AccountPassword*

Specifies a new password value for an account. This value is stored as an encrypted string. Using `ConvertTo-SecureString` allows for the password to be passed as part of the `ForEach-Object` loop.

### *[ConvertTo-SecureString](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/convertto-securestring?view=powershell-6)*

Converts encrypted standard strings to secure strings. I have used it to convert plain text to a secure string.

*Not recommended to be used in production as the string is in plain text.*

### *-AsPlainText*

Specifies a plain text string to convert to a secure string.

*Not recommended to be used in production as the string is in plain text.*

### *-Force*

Confirms that you understand the implications of using the *AsPlainText* parameter.

*Not recommended to be used in production as the string is in plain text.*

### *[Get-ADUser](https://docs.microsoft.com/en-us/powershell/module/addsadministration/get-aduser?view=win10-ps)*

Gets one or more Active Directory users.

### *-Filter*

Specifies a query string that retrieves Active Directory objects. I'm using `*` as a wildcard character.

### *-SearchBase*

Specifies an Active Directory path to search under.

### *[Remove-ADUser](https://docs.microsoft.com/en-us/powershell/module/activedirectory/remove-aduser?view=winserver2012-ps)*

Removes and Active Directory user.

### *-Confirm*

Prompts you for confirmation before running the cmdlet. I have used `-Confirm:$false` to remove the prompt for confirmation before removal.

## Conclusion

The above is a quick and convenient way to generate generic users quickly. This can be very useful when you need multiple users to test against.

Hope you're having a great day and this is of use.

Thanks, Tim.
