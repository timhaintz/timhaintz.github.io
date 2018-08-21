---
layout: post
title: "CSV to Confluence Markdown"
date: 2018-08-21
---

### Introduction
The below script is used to convert a CSV file into a Confluence markdown table. The Confluence markdown table format used is Table 1 from [Confluence Wiki Markup](https://confluence.atlassian.com/doc/confluence-wiki-markup-251003035.html#ConfluenceWikiMarkup-Tables).

### Script
#### PowerShell Code Block
```PowerShell
$date = (Get-Date -Format yyyyMMdd)
$input = (Get-Content $env:TEMP\$date`_AutoDoco.csv)
$contents = $input
$header = $contents[0]
$outputlocation = "$env:TEMP\$date`_AutoDoco.md"

foreach($content in $contents)
{
    if($content -eq $header)
    {
        $content = $content.replace('"','||')
        $content = $content.replace(',','')
        $content = $content.replace('||||','||')
        Out-File -FilePath $outputlocation -Append -NoClobber -InputObject $content
    }
    else
    {
        $content = $content.replace('"','|')
        $content = $content.replace(',','')
        $content = $content.replace('||','|')
        $content = $content.replace("`t"," * ")
        Out-File -FilePath $outputlocation -Append -NoClobber -InputObject $content
    }
    # end region
}
#end region
```
### Explanation
The conversion takes a CSV file *$input = (Get-Content $env:TEMP\$date`_AutoDoco.csv)* and then uses string manipulation to format the content. If the content is a header *$header = $contents[0]* & *if($content -eq $header)* it will replace *"* with *||*, replace the *,* with blank and then remove any instance of *||||* and replace it with *||*. *[Out-File](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-6)* is then used to write the string to a file at *$outputlocation* and use *$content* as the InputObject. *Out-File* creates a new line by default.

If the content is not a header, the else statement is invoked and replaces " with \|. The , is replaced with blank and any instance of || is replaced with a single \| . *[Out-File](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-6)* is then used to write the string to a file at *$outputlocation* and use *$content* as the InputObject. *Out-File* creates a new line by default.

### Example
I ran *[Get-Service](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-service?view=powershell-6)*
as an example to show the conversion.

#### PowerShell Code Block
```PowerShell
Get-Service | Select-Object -First 5 -Property Name,DisplayName,Status,ServiceType | Export-CSV $env:TEMP\20180821_AutoDoco.csv

# Contents of CSV file
"Name","DisplayName","Status","ServiceType"
"AdobeARMservice","Adobe Acrobat Update Service","Running","Win32OwnProcess"
"AJRouter","AllJoyn Router Service","Stopped","Win32ShareProcess"
"ALG","Application Layer Gateway Service","Stopped","Win32OwnProcess"
"ApHidMonitorService","Alps HID Monitor Service","Running","Win32OwnProcess"
"AppIDSvc","Application Identity","Stopped","Win32ShareProcess"

# Contents of file after running the conversion script and changing it to an MD file
||Name||DisplayName||Status||ServiceType||
|AdobeARMservice|Adobe Acrobat Update Service|Running|Win32OwnProcess|
|AJRouter|AllJoyn Router Service|Stopped|Win32ShareProcess|
|ALG|Application Layer Gateway Service|Stopped|Win32OwnProcess|
|ApHidMonitorService|Alps HID Monitor Service|Running|Win32OwnProcess|
|AppIDSvc|Application Identity|Stopped|Win32ShareProcess|
```

#### Confluence Wiki output
![Confluence Wiki]({{ "/assets/20180821/1-ConfluenceWiki.png" | absolute_url }})


### Cmdlets used
### *Out-File*
Sends output to a file. 

### *-FilePath*
Specifies the path to the output file.

### *-Append*
Adds output to the end of an existing file, instead of replacing the file contents.

### *-NoClobber*
Will not overwrite an existing file.

### *-InputObject*
Specifies the objects to be written to the file.

### *Get-Service*
Gets objects that represent the services on a computer.

### *Select-Object*
Selects specified properties of an object or set of objects. It can also select unique objects, a specified number of objects, or objects in a specified position in an array.

### *-First*
Gets only the specified number of objects.

### *-Property*
Specified the properties to select.

### Conclusion
Hopefully the above has given you some ideas on how you can use string manipulation to convert a CSV file into a Confluence Wiki Markdown Table. This is a great way to present information gathered from a CSV via a webpage.

Hope you're having a great day and this is of use.

Thanks, Tim.
