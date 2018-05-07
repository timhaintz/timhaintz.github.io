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

This isn't particularly useful to put in as a filename. 

Luckily for us, Get-Date has a -Format parameter, which can be used to display the date in a number of ways.

For example:
```PowerShell
Get-Date -Format yyMMdd
180507
```
