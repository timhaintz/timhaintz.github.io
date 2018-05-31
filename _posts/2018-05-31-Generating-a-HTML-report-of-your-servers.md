---
layout: post
title: "Generating a HTML Report of your servers"
date: 2018-05-31
---
## Generating a HTML report of your servers

Below is an example of some of the data that you can retrieve from Get-ADComputer about a server. I'm outputting this information to a HTML document.
This script is also slightly interactive as it uses [Write-Host](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/write-host?view=powershell-6). This is for visual feedback in an interactive environment. Note that Write-Host isn't able to output to another script or be re-used. Inventor of PowerShell, Jeffrey Snover, has a great article [here](http://www.jsnover.com/blog/2013/12/07/write-host-considered-harmful/) about using Write-Host. 

The script is below. Copy it and save it as a .PS1 file. After the script, I break down what each section of the script does.

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
$servers = $ous | ForEach-Object { Get-ADComputer -Filter * -Properties * -SearchBase $_ }
$servers = $servers | Where-Object{$_.dnshostname} | Sort-Object -Property 'CN'

Write-Host "Retreived servers from OUs and sorted machines based on server name"

#$frag is a fragment used for ConvertTo-Html. It contains the interesting information.
$frag = foreach ($server in $servers)
{
    Write-Host $server.cn
    #If Test-Connection is false (that's what ! in the if statement means) then pass into the if statement.
    if(!(Test-Connection -ComputerName $server.dnshostname -Count 1 -Quiet))
    {
        $server | Select-Object -Property @{Label='Computer Name'; Expression ={$_.cn}},IPv4Address,whenCreated,whenChanged                               
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

Breaking out each of the parts below.

### CSS, Date and File Format

I'm using CSS to style my HTML page. The CSS is being stored as the $head variable. This is used later on in [ConvertTo-Html](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/convertto-html?view=powershell-6) with the -Head parameter. 

I also like to store the date in a specific format. The date is then used to generate the file name. 
Storing the date as yyyyMMdd (20180531) for example allows the files to be sorted nicely in date order.
I also use the $env:TEMP variable as whoever is running the script has permission to this location. 
As below, the file will be called 20180531_test and will be located in $env:TEMP. In my test environment, $env:TEMP is: C:\Users\AZUREA~1\AppData\Local\Temp

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

### Capturing the Servers and Their Properties

Get-ADComputer can't search multiple OUs with the -SearchBase parameter. For this reason, we have to store the OUs as separate strings and then run them through the [ForEach-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/foreach-object?view=powershell-6) cmdlet.

$ous = 'CN=Computers,DC=timhaintz,DC=com','OU=Domain Controllers,DC=timhaintz,DC=com' is where I have the computers stored in Active Directory.

$servers = $ous | ForEach-Object { Get-ADComputer -Filter * -Properties * -SearchBase $_ } searches through each of the OUs for the machines I'm looking for and stores them in the $servers variable.
Get-ADComputer cmdlet, I'm using -Filter * and -Properties * to retrive all machines and also all information about those machines.

$servers = $servers | Where-Object{$_.dnshostname} | Sort-Object -Property 'CN'
Checks that the computer object contains a dnshostname value. I also use [Sort-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/sort-object?view=powershell-6) to sort the list of servers from their CN value or server name.

Write-Host is being used to present feedback to the user running the script.

```PowerShell
$ous = 'CN=Computers,DC=timhaintz,DC=com','OU=Domain Controllers,DC=timhaintz,DC=com'

Write-Host "OUs being used to search are: $($ous)"

$servers = $ous | ForEach-Object { Get-ADComputer -Filter * -properties * -SearchBase $_ }
$servers = $servers | Where-Object{$_.dnshostname} | Sort-Object -Property 'CN'

Write-Host "Retreived servers from OUs and sorted machines based on server name"
```

### Create Fragment for ConvertTo-Html

Using the [ForEach](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_foreach?view=powershell-6) statement I loop through each server that was collected in $servers.

Again, I'm using Write-Host to provide feedback to the person running the script.

Using an [If](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_if?view=powershell-6) statement and Test-Connection, logic can be used to decide what information to look for. Below, I'm using if(!(Test-Connection -Quiet)). The ! reverses the logic to be NOT. -Quiet returns a [boolean](https://blogs.msdn.microsoft.com/powershell/2006/12/24/boolean-values-and-operators/) value. If Test-Connection fails, with the ! mark, the if statement evaluates TRUE and enters the if statement. Remove the ! and it will capture the information of servers where Test-Connection is successful.

To present the HTML report with nice labels, I'm using [Select-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-6) and a calculated property to rename the property from cn to Computer Name. @{Label='Computer Name'; Expression ={$_.cn}} is the calculated property. I'm also selecting IPv4Address, whenCreated and whenChanged. Anything that is gathered from Get-ADComputer -Properties * can be used in Select-Object -Property.
For example, badPwdCount or LastLogonDate could also be included if that information was of interest.

The results of $server | Select-Object ... are stored in the $frag variable to be used later with ConvertTo-Html.

```PowerShell
#$frag is a fragment used for ConvertTo-Html. It contains the interesting information.
$frag = foreach ($server in $servers)
{
    Write-Host $server.cn
    #If Test-Connection is false (that's what ! in the if statement means) then pass into the if statement.
    if(!(Test-Connection -ComputerName $server.dnshostname -Count 1 -Quiet))
    {
        $server | Select-Object -Property @{Label='Computer Name'; Expression ={$_.cn}},IPv4Address,whenCreated,whenChanged                               
    }
}
```

### Generating and Saving the HTML Report

$frag is piped into ConvertTo-Html. Using the -Title, -PreContent, and -Head parameters of ConvertTo-Html, the CSS in $head is used to present the $frag information and display it in a table.

In my test environment, the contents of $frag is as below:

```PowerShell
PS C:\Users\azureadmin\Documents> $frag

Computer Name IPv4Address whenCreated          whenChanged         
------------- ----------- -----------          -----------         
Srv1          10.0.0.8    5/31/2018 8:06:30 PM 5/31/2018 8:07:20 PM
Srv2          10.0.0.7    5/30/2018 8:39:30 PM 5/30/2018 8:40:21 PM
```

This information is then piped to [Out-File](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-6) and saved to $outputlocation.

I then call [Invoke-Item](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/invoke-item?view=powershell-6) $outputlocation to open the HTML document automatically.

```PowerShell
#Convert captured servers into HTML as per formatting and information required.
$frag | ConvertTo-Html -Title 'Failed PING of Servers' `
                       -PreContent "<h1>Below are the $($frag.count) servers that failed a PING test. $($servers.count) servers were pinged in this process.</h1>" `
                       -Head $head |
        Out-File $outputlocation
        Write-Host "File written to: $outputlocation"
        Invoke-Item $outputlocation
```

A screenshot of the report from my test environment is shown below:

![HTML Report]({{ "/assets/20180531/HTML-Report.png" | absolute_url }})

This is a nice visual way of displaying if any of your servers or computers are no longer 'pingable' and may need attention.

Hope you're having a great day and this is of use.

Thanks, Tim.
