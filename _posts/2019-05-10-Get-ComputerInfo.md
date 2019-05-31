---
layout: default
title: "Get-ComputerInfo"
date: 2019-05-10
---
# {{ page.title }}

## Introduction

It has been a while since my last post, life got in the way of blogging for few months. Will be back blogging more regularly again.

I found out about a cmdlet recently that I can't believe I never knew about. The cmdlet is [Get-ComputerInfo](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-computerinfo?view=powershell-6). Thanks to Don for letting me know about it.
The cmdlet was released in Windows PowerShell 5.1.

### Script

#### PowerShell Code Block

```powershell
Get-ComputerInfo
```

## Results

Below is a small sample of the output.

```powershell
WindowsBuildLabEx                                       : 17763.1.amd64fre.rs5_release.180914-1434
WindowsCurrentVersion                                   : 6.3
WindowsEditionId                                        : ServerDatacenterEval
WindowsInstallationType                                 : Server
WindowsInstallDateFromRegistry                          : 6/05/2019 8:51:28 AM
WindowsProductId                                        : 00431-20000-00000-AA661
WindowsProductName                                      : Windows Server 2019 Datacenter Evaluation
WindowsRegisteredOrganization                           :
WindowsRegisteredOwner                                  :
WindowsSystemRoot                                       : C:\Windows
WindowsVersion                                          : 1809
BiosCharacteristics                                     : {4, 7, 9, 11...}
BiosBIOSVersion                                         : {VRTUAL - 6001702, BIOS Date: 06/02/17 12:52:12  Ver: 09.00.07, BIOS Date: 06/02/17 12:52:12  Ver:
                                                          09.00.07}
BiosBuildNumber                                         :
BiosCaption                                             : BIOS Date: 06/02/17 12:52:12  Ver: 09.00.07
BiosCodeSet                                             :
BiosCurrentLanguage                                     : enUS
BiosDescription                                         : BIOS Date: 06/02/17 12:52:12  Ver: 09.00.07
BiosEmbeddedControllerMajorVersion                      :
BiosEmbeddedControllerMinorVersion                      :
BiosFirmwareType                                        : Bios
BiosIdentificationCode                                  :
BiosInstallableLanguages                                : 1
BiosInstallDate                                         :
BiosLanguageEdition                                     :
BiosListOfLanguages                                     : {enUS}
BiosManufacturer                                        : American Megatrends Inc.
```

## Conclusion

If you're looking for information about your system and you have Windows PowerShell 5.1 or 6, `Get-ComputerInfo` is a great place to start.
You might not need to use [Get-CimInstance](https://docs.microsoft.com/en-us/powershell/module/cimcmdlets/get-ciminstance?view=powershell-6) or  [Get-WMIObject](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-wmiobject?view=powershell-5.1). Hopefully you can save some time using `Get-ComputerInfo`

Hope you're having a great day and this is of use.

Thanks, Tim.
