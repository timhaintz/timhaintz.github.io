---
layout: post
title: "How to save a file with today's date in it: Get-Date"
date: 2018-05-07
---

Often, when running a regular report, I like to keep the date in the name of the output file. This removes any potential file overwrite issues and is a good visual indicator of the history of the job.

To do this, I use the [Get-Date](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-date?view=powershell-6) cmdlet. 

By default, Get-Date outputs as below:
```PowerShell
Get-Date
Monday, May 7, 2018 9:19:08 PM
```

This isn't particularly useful to put in a filename. 

Luckily for us, Get-Date has a -Format parameter. The -Format parameter can be used to display the date in a number of ways.

For example:
```PowerShell
Get-Date -Format yyMMdd
180507
```

To use it in a file name, I like to save the date in the desired format as a variable and then use it in the filename.

```PowerShell
$dateyyMMdd = Get-Date -Format yyMMdd
Get-Process > $dateyyMMdd-Process.txt

PS C:\Users\azureadmin\test> ls


    Directory: C:\Users\azureadmin\test


Mode                LastWriteTime         Length Name                                                                             
----                -------------         ------ ----                                                                             
-a----         5/7/2018   9:34 PM          16382 180507-Process.txt
```
