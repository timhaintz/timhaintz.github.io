---
layout: post
title: "CSV to Confluence Markdown"
date: 2018-08-17
---

### Introduction
The below script is used to convert a CSV file into a Confluence markdown table. The Confluence markdown table format I used is Table 1 from [Confluence Wiki Markup](https://confluence.atlassian.com/doc/confluence-wiki-markup-251003035.html#ConfluenceWikiMarkup-Tables).

### Script
#### PowerShell Code Block
```PowerShell
$contents = (Get-Content $env:TEMP\CSVtoMkDown.csv)
$header = $contents[0]
$date = Get-Date -Format yyyyMMdd
$outputlocation = "$env:TEMP\$date`_AutoDoco.md"

foreach($content in $contents)
{
    if($content -eq $header)
    {
        $headersplit = $header -split(',')
        $content -split(',') |
        ForEach-Object {
            if($_ -eq $headersplit[-1])
            {
                $_ = $_.replace('"','')
                $_ = "||$_||`n"
            }
            else
            {
                $_ = $_.replace('"','')
                $_ = "||$_"
            } 
            Write-Output $_
        } |
        Out-File -FilePath $outputlocation -Append -NoClobber -NoNewline
        # end region
    }
    # end region
    else 
    {
        $contentsplit = $content -split(',')
        $content -split(',') |
        ForEach-Object {
            if($_ -eq $contentsplit[-1])
            {
                $_ = $_.replace('"','')
                $_ = "|$_|`n"
            }
            else
            {
                $_ = $_.replace('"','')
                $_ = "|$_"
            }
            Write-Output $_
        } |
        Out-File -FilePath $outputlocation -Append -NoClobber -NoNewline
        # end region
    }
    #end region
}
#end region
```
### Explanation
The conversion takes a CSV file *$contents = (Get-Content $env:TEMP\CSVtoMkDown.csv)* and then uses string manipulation to format the content. If the content is a header *$header = $contents[0]* & *if($content -eq $header)* it will place || around each column value.

### Cmdlets used
### *Cmdlet 1*

### *-Paramater 1*

### *-Paramater 2*

### *-Paramater N*

### *Cmdlet N*

### *-Paramater 1*

### *-Paramater 2*

### *-Paramater N*

### Insert Assets
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})

### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
