---
layout: default
title: "How many test users would you like?"
date: 2019-02-12
---
# {{ page.title }}

## Introduction

When testing it is usefull to be able to create and destroy users repeatedly. A straight forward method I use to create any number of users is using the PowerShell *Range operator* `..`. This allows me to pipe the range of numbers into the `ForEach-Object` cmdlet.

### Script

#### PowerShell Code Block

```powershell
New-ADOrganizationalUnit -Name "Employees" -Path "DC=TIMHAINTZ,DC=COM"

1..10 | ForEach-Object {New-AdUser -Name "User-$_" -samAccountname "User-$_" -UserPrincipalName "User-$_`@timhaintz.com" -Path "OU=Employees,DC=timhaintz,DC=com" -enabled $true -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -force)}

```

## Results

```powershell

```

## Explanation

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
