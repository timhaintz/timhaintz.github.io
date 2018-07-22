---
layout: post
title: "PowerCLI - Installation"
date: 2018-07-25
---
## PowerCLI - Installation
VMware [PowerCLI](https://www.vmware.com/support/developer/PowerCLI/) is a command-line and scripting tool built on Windows Powershell.

To install PowerCLI, you first need to download it. As of this writing, the current version is [VMware PowerCLI 10.1.1](https://code.vmware.com/web/dp/tool/vmware-powercli/10.1.1).
The [VMware PowerCLI User's Guide](https://vdc-download.vmware.com/vmwb-repository/dcr-public/76e07a15-f457-47a0-a16c-0db7bd31bda8/9d37ff69-25de-45d9-80c1-16a1f429b86e/vmware-powercli-1011-user-guide.pdf), available from the download link above, has further information and installation instructions.

You can also install PowerCLI via the [PowerShell Gallery](https://www.powershellgallery.com/). The [VMware PowerCLI Blog](https://blogs.vmware.com/PowerCLI/2017/04/powercli-install-process-powershell-gallery.html) has a good write up on how to install via this method. 

Installing PowerCLI via PowerShell gallery is below.

### Script
#### PowerShell Code Block
```PowerShell
Find-Module VMware.PowerCLI

Version    Name                                Repository           Description                                                                                               
-------    ----                                ----------           -----------                                                                                               
10.1.1.... VMware.PowerCLI                     PSGallery            This Windows PowerShell module contains VMware.PowerCLI 

Install-Module -Name VMware.PowerCLI
```

### Results
```PowerShell
Get-Module VMware.PowerCLI
```

### Explanation

#### *Cmdlet 1*

#### *-Paramater 1*

#### *-Paramater 2*

#### *-Paramater N*

#### *Cmdlet N*

#### *-Paramater 1*

#### *-Paramater 2*

#### *-Paramater N*



### Insert Assets
![HTML Report]({{ "/assets/20180531/HTML-EmailAsFile.png" | absolute_url }})

### Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
