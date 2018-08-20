---
layout: post
title: "CSV to Confluence Markdown"
date: 2018-08-20
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
The conversion takes a CSV file *$input = (Get-Content $env:TEMP\$date`_AutoDoco.csv)* and then uses string manipulation to format the content. If the content is a header *$header = $contents[0]* & *if($content -eq $header)* it will replace *"* with *||*, replace the *,* with blank and then remove any instance of *||||* and replace it with *||*. *[Out-File](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-6)* is then used to write the string to a file at *$outputlocation* and use *$content* as the InputObject. Out-File creates a new line by default.

If the content is not a header, the else statement is invoked and replaces *"* with *|*. The *,* is replaced with blank and any instance of *||* is replaced with a single *|*. *[Out-File](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-6)* is then used to write the string to a file at *$outputlocation* and use *$content* as the InputObject. Out-File creates a new line by default.

### Cmdlets used
### *Out-File*

### *-Paramater 1*

### *-Paramater 2*

### *-Paramater N*

### Insert Assets
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})

### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
