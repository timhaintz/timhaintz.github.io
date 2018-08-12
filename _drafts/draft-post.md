---
layout: post
title: "Template Title"
date: 2018-08-15
---

### Introduction
The below script is used to convert a CSV file to a Confluence markdown table. The Confluence markdown table format I used is Table 1 from [Confluence Wiki Markup](https://confluence.atlassian.com/doc/confluence-wiki-markup-251003035.html#ConfluenceWikiMarkup-Tables).

### Script
#### PowerShell Code Block
```PowerShell
$input = (Get-Content $env:TEMP\CSVtoMkDown.csv)
$header = $contents[0]

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
        Out-File -FilePath $env:TEMP\markdown.md -Append -NoClobber -NoNewline
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
        Out-File -FilePath $env:TEMP\markdown.md -Append -NoClobber -NoNewline
        # end region
    }
    #end region
}
#end region
```

### Results
```PowerShell

```

### Explanation

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
