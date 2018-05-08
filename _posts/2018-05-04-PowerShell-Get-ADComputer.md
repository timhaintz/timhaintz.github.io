---
layout: post
title: "PowerShell ActiveDirectory Module & Get-ADComputer"
date: 2018-05-04
---
## Get-ADComputer
I'm often looking up workstation and/or server details. This can be tedious if I have to open up *Active Directory Users and Computers* and *Find* every time. PowerShell to the rescue! If I don't know the exact name, something I use often is the -Filter parameter from the [Get-ADComputer](https://docs.microsoft.com/en-us/powershell/module/addsadministration/get-adcomputer?view=win10-ps) [cmdlet](https://msdn.microsoft.com/en-us/library/ms714395(v=vs.85).aspx).

```PowerShell
Get-ADComputer -Filter {name -like '*a*'}
```
Returns:
```PowerShell
PS C:\Users\azureadmin> Get-ADComputer -Filter {name -like '*a*'}


DistinguishedName : CN=ca1,CN=Computers,DC=timhaintz,DC=com
DNSHostName       : ca1.timhaintz.com
Enabled           : True
Name              : ca1
ObjectClass       : computer
ObjectGUID        : 3d0102ae-11fd-4f3c-8f72-a67356b46c61
SamAccountName    : CA1$
SID               : S-1-5-21-493708430-333671045-2630090032-1103
UserPrincipalName :
```


## From Windows 10
If you are using Windows 10, you will need to install [Remote Server Administration Tools (RSAT) for Windows 10](https://www.microsoft.com/en-au/download/details.aspx?id=45520) and then enable RSATClient-Roles-AD-Powershell before you can access the [ActiveDirectory Module](https://docs.microsoft.com/en-us/powershell/module/addsadministration/?view=win10-ps) [cmdlets](https://msdn.microsoft.com/en-us/library/ms714395(v=vs.85).aspx). [Install the Active Directory PowerShell Module on Windows 10 by Ashley McGlone](https://blogs.technet.microsoft.com/ashleymcglone/2016/02/26/install-the-active-directory-powershell-module-on-windows-10/) has a scriptable way to install RSAT.

## Steps to run the ActiveDirectory module from Windows 10.
1. Install RSAT
2. 
```PowerShell
Get-WindowsOptionalFeature -Online -FeatureName RSATClient-Roles-AD-Powershell
```
3. You will now be able to use the ActiveDirectory module from your Windows 10 machine.

Thanks, Tim.
