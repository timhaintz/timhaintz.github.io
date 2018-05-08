---
layout: post
title: "Copying files to other machines: New-PSSession & Copy-Item"
date: 2018-05-08
---
## New-PSSession and Copy-Item
On occassion, files need to be copied from one machine to another. This can include times where the machines are in different domains, or elevated permissions are required to fulfil the task. There are quite a few methods to do this. 

Below, I use [Get-Credential](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential?view=powershell-6), [New-PSSession](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/new-pssession?view=powershell-6) and [Copy-Item](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/copy-item?view=powershell-6). 
The folder and file layout on my local machine is as below:

```PowerShell
PS C:\Users\azureadmin\test> $env:COMPUTERNAME
ca1

PS C:\Users\azureadmin\test> ls -Recurse

    Directory: C:\Users\azureadmin\test

Mode                LastWriteTime         Length Name                               
----                -------------         ------ ----
d-----         5/8/2018   8:32 PM                Info                                                                                    
    Directory: C:\Users\azureadmin\test\Info

Mode                LastWriteTime         Length Name 
----                -------------         ------ ---- 
d-----         5/8/2018   8:32 PM                Folder1  
d-----         5/8/2018   8:32 PM                Folder2 

    Directory: C:\Users\azureadmin\test\Info\Folder1

Mode                LastWriteTime         Length Name 
----                -------------         ------ ----   
-a----         5/8/2018   8:32 PM             14 Test1.txt   
-a----         5/8/2018   8:32 PM              0 Test2.txt                                                                                                              

    Directory: C:\Users\azureadmin\test\Info\Folder2

Mode                LastWriteTime         Length Name    
----                -------------         ------ ----     
-a----         5/8/2018   8:32 PM              0 Test3.txt  
-a----         5/8/2018   8:32 PM              0 Test4.txt
```


```PowerShell


```


