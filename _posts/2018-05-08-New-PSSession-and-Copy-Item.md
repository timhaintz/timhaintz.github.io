---
layout: post
title: "Copying files to other machines: New-PSSession & Copy-Item"
date: 2018-05-08
---
## New-PSSession and Copy-Item
On occassion, files need to be copied from one machine to another. This can include times where the machines are in different domains, or elevated permissions are required to fulfil the task. There are quite a few methods to do this. 

Below, I use [Get-Credential](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential?view=powershell-6), [New-PSSession](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/new-pssession?view=powershell-6) and [Copy-Item](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/copy-item?view=powershell-6). From the *Notes* section of the New-PSSession documentation **This cmdlet uses the Windows PowerShell remoting infrastructure. To use this cmdlet, the local computer and any remote computers must be configured for Windows PowerShell remoting.** Please ensure [PowerShell Remoting](https://docs.microsoft.com/en-us/powershell/scripting/core-powershell/running-remote-commands?view=powershell-6#windows-powershell-remoting) is setup.

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
To copy the folders and files, the below PowerShell commands are run.

```PowerShell
$credential = Get-Credential timhaintz\azureadmin
$session = New-PSSession -ComputerName dc1 -Credential $credential
Copy-Item -Recurse "C:\Users\azureadmin\test" -Destination "C:\test\" -ToSession $Session
```
The first line $credential = Get-Credential...... prompts for a username and password. In a future blog, I will use [Export-Clixml](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/export-clixml?view=powershell-6) to export the credentials into an XML file, so as to remove the need for user interaction.

The New-PSSession example is taken straight from Microsoft's documenation, as is Copy-Item.

To interactively connect to the destination server [Enter-PSSession](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-6) can be utilised. 

```PowerShell
PS C:\Users\azureadmin\test> Enter-PSSession -Session $session

[dc1]: PS C:\test> 
```
From this session, you can check if the files and folders copied correctly.

```PowerShell
[dc1]: PS C:\test> $env:COMPUTERNAME
dc1

[dc1]: PS C:\test> ls -Recurse


    Directory: C:\test


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         5/8/2018   8:36 PM                Info


    Directory: C:\test\Info


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         5/8/2018   8:36 PM                Folder1
d-----         5/8/2018   8:36 PM                Folder2


    Directory: C:\test\Info\Folder1


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         5/8/2018   8:32 PM             14 Test1.txt
-a----         5/8/2018   8:32 PM              0 Test2.txt


    Directory: C:\test\Info\Folder2


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         5/8/2018   8:32 PM              0 Test3.txt
-a----         5/8/2018   8:32 PM              0 Test4.txt
```
As displayed above, the folders and files from the local machine are successfully copied to the destination machine using a session.

Hope this is of use.

Thanks, Tim.
