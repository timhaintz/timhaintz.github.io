---
layout: post
title: "HTML Report for servers"
date: 2018-05-24
---
## HTML Report

Generating a HTML report of your servers.

Below is an example of some of the data that you can retrieve from a server. I'm outputting this information as HTML.

```PowerShell
<#
    Created by  : Tim Haintz
    Date Created: 24/05/2017
    
    Description : Produce an HTML report of all production servers pinged but not responding.

    URLs used   :
    https://technet.microsoft.com/en-us/library/ff730936.aspx
    https://powershell.org/2012/10/24/free-ebook-creating-html-reports-in-powershell/
    https://leanpub.com/creatinghtmlreportsinpowershell
    https://www.w3schools.com/css/


#>

# CSS Styles for HTML output
$head = "
<style>
BODY{background-color:white;}
TABLE{border-width: 1px;border-style: solid;border-color: black;border-collapse: collapse;}
TH{border-width: 1px;padding: 0px;border-style: solid;border-color: black;background-color:LightSteelBlue}
TD{border-width: 1px;padding: 0px;border-style: solid;border-color: black;background-color:LightCoral}
.success{background-color:#ff3333;}
.failure{background-color:#66ff99;}
</style>
"
# Date format correct for saving in the output location. A new file will be created each new day/date
$date = (Get-Date -Format yyyyMMdd)
$outputlocation = "$env:TEMP\$date`_test.html"



#$frag is a fragment used for ConvertTo-Html. It contains the interesting information.
$frag = foreach ($server in $servers)
{
    Write-Host $server.cn
    #If Test-Connection is false (that's what ! in the if statement means) then pass into the if statement.
    if(!(Test-Connection -ComputerName $server.dnshostname -Count 1 -Quiet))
    {
        $server | Select-Object -Property @{Label='Computer Name'; expression ={$_.cn}},IPv4Address,whenCreated,whenChanged                               
    }
}
#Convert captured servers into HTML as per formatting and information required.
$frag | ConvertTo-Html -Title 'Failed PING of Servers' `
                       -PreContent "<h1>Below are the $($frag.count) servers that failed a PING test. $($servers.count) servers were pinged in this process.</h1>" `
                       -Head $head |
        Out-File "$env:TEMP\$date`_test.html"
        Write-Host "File written to: $env:TEMP\$date`_test.html"
        Invoke-Item "$env:TEMP\$date`_test.html"
```

Hope you're having a great day and this is of use.

Thanks, Tim.
