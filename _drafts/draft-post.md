---
layout: post
title: "HTML Report for servers"
date: 2018-05-24
---
## Generating a HTML report of your servers

Below is an example of some of the data that you can retrieve from a server. I'm outputting this information to a HTML document.
This script is also slightly interactive as I'm using [Write-Host](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/write-host?view=powershell-6). This is for visual feedback in an interactive environment. Note that Write-Host isn't able to output to another script or be re-used. Inventor of PowerShell Jeffrey Snover has a great article [here](http://www.jsnover.com/blog/2013/12/07/write-host-considered-harmful/) about Write-Host. 

Using an If statement with Test-Connection, I'm also checking if the server responds to a ping or in this case, not responding.

The script is below. Copy it and save it as a .PS1 file. Below, I break down what each section of the script does.

```PowerShell
<#
    Created by  : Tim Haintz
    Date Created: 24/05/2017
    
    Description : Produce an HTML report of all servers pinged but not responding.

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
</style>
"
# Date format correct for saving in the output location. A new file will be created each new day/date
$date = (Get-Date -Format yyyyMMdd)
$outputlocation = "$env:TEMP\$date`_test.html"

<#
Used if you would like to put individual machines in rather than using OUs
$computernames = 'dc1','ca1'

$servers = foreach ($computername in $computernames)
           {
               Get-ADComputer $computername -Properties *
               
           }
#>

$ous = 'CN=Computers,DC=timhaintz,DC=com','OU=Domain Controllers,DC=timhaintz,DC=com'

Write-Host "OUs being used to search are: $($ous)"

#$servers being populated from the OUs with all of their AD attributes. 
#$servers is then filtered using where-object to only objects that contain .dnshostname entries as these are 'real' machines
#$servers is then sorted alphabetically based on CN/hostname. 
$servers = $ous | ForEach-Object { Get-ADComputer -Filter * -properties * -SearchBase $_ }
$servers = $servers | Where-Object{$_.dnshostname} | Sort-Object -Property 'CN'

Write-Host "Retreived servers from OUs and sorted machines based on server name"

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
        Out-File $outputlocation
        Write-Host "File written to: $outputlocation"
        Invoke-Item $outputlocation
```

Breaking out each of the parts below, I will explain what each is doing.

### CSS and date and file format
I'm using CSS to style my HTML page. The CSS is being stored as the $head variable. This is used later on in [ConvertTo-Html](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/convertto-html?view=powershell-6) with the -Head parameter. 

I also like to store the date in a specific format. The date is then used to generate the file name. 
Storing the date as yyyyMMdd (20180530) for example allows the files to be sorted nicely in date order.
I also use the $env:TEMP variable as whoever is running the script has permission to this location. 
As below, the file will be called 20180530_test and will be located in $env:TEMP. In my test environment, this is: C:\Users\AZUREA~1\AppData\Local\Temp

```PowerShell
# CSS Styles for HTML output
$head = "
<style>
BODY{background-color:white;}
TABLE{border-width: 1px;border-style: solid;border-color: black;border-collapse: collapse;}
TH{border-width: 1px;padding: 0px;border-style: solid;border-color: black;background-color:LightSteelBlue}
TD{border-width: 1px;padding: 0px;border-style: solid;border-color: black;background-color:LightCoral}
</style>
"
# Date format correct for saving in the output location. A new file will be created each new day/date
$date = (Get-Date -Format yyyyMMdd)
$outputlocation = "$env:TEMP\$date`_test.html"
```

Hope you're having a great day and this is of use.

Thanks, Tim.
