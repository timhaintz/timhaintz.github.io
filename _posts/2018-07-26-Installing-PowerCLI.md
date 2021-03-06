---
layout: default
title: "Installing PowerCLI"
date: 2018-07-26
---
# {{ page.title }}

## Introduction

VMware [PowerCLI](https://www.vmware.com/support/developer/PowerCLI/) is a command-line and scripting tool built on Windows Powershell.

To install PowerCLI, you first need to download it. As of this writing, the current version is [VMware PowerCLI 10.1.1](https://code.vmware.com/web/dp/tool/vmware-powercli/10.1.1).
The [VMware PowerCLI User's Guide](https://vdc-download.vmware.com/vmwb-repository/dcr-public/76e07a15-f457-47a0-a16c-0db7bd31bda8/9d37ff69-25de-45d9-80c1-16a1f429b86e/vmware-powercli-1011-user-guide.pdf), available from the download link above, has further information and installation instructions.

The [VMware PowerCLI Blog](https://blogs.vmware.com/PowerCLI/2017/04/powercli-install-process-powershell-gallery.html) has a good write up on how to install via this method.

Installing from PowerShell via [PowerShell Gallery](https://www.powershellgallery.com/) is below.

### Script

#### PowerShell Code Block

![NuGet](/assets/20180725/1-NuGet.png)

```powershell
Find-Module -Name VMware.PowerCLI

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
10.1.1.... VMware.PowerCLI                     PSGallery            This Windows PowerShell module contains VMware.PowerCLI
```

![VMware warning](/assets/20180725/3-Install-Module-VMware-Warning.png)

```powershell
Install-Module -Name VMware.PowerCLI
```

![Installation Progress](/assets/20180725/4-Installation-Progress.png)

## Results

```powershell
Get-Module -Name VMware* -ListAvailable

    Directory: C:\Program Files\WindowsPowerShell\Modules

ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Script     6.7.0.8... VMware.DeployAutomation             {Add-DeployRule, Add-ProxyServer, Add-ScriptBundle, Copy-DeployRule...}
Script     6.7.0.8... VMware.ImageBuilder                 {Add-EsxSoftwareDepot, Add-EsxSoftwarePackage, Compare-EsxImageProfile, Export-EsxImageProfile...}
Manifest   10.1.1.... VMware.PowerCLI
Script     6.7.0.8... VMware.Vim
Script     10.1.0.... VMware.VimAutomation.Cis.Core       {Connect-CisServer, Disconnect-CisServer, Get-CisService}
Script     10.0.0.... VMware.VimAutomation.Cloud          {Add-CIDatastore, Connect-CIServer, Disconnect-CIServer, Get-Catalog...}
Script     10.1.0.... VMware.VimAutomation.Common
Script     10.1.0.... VMware.VimAutomation.Core           {Add-PassthroughDevice, Add-VirtualSwitchPhysicalNetworkAdapter, Add-VMHost, Add-VMHostNtpServer...}
Script     6.5.4.7... VMware.VimAutomation.HA             Get-DrmInfo
Script     7.5.0.8... VMware.VimAutomation.HorizonView    {Connect-HVServer, Disconnect-HVServer}
Script     10.0.0.... VMware.VimAutomation.License        Get-LicenseDataManager
Script     10.1.0.... VMware.VimAutomation.Nsxt           {Connect-NsxtServer, Disconnect-NsxtServer, Get-NsxtService}
Script     10.0.0.... VMware.VimAutomation.PCloud         {Connect-PIServer, Disconnect-PIServer, Get-PIComputeInstance, Get-PIDatacenter}
Script     10.1.0.... VMware.VimAutomation.Sdk
Script     10.0.0.... VMware.VimAutomation.Srm            {Connect-SrmServer, Disconnect-SrmServer}
Script     10.1.0.... VMware.VimAutomation.Storage        {Add-KeyManagementServer, Copy-VDisk, Export-SpbmStoragePolicy, Get-KeyManagementServer...}
Script     1.2.0.0    VMware.VimAutomation.StorageUtility Update-VmfsDatastore
Script     10.1.0.... VMware.VimAutomation.Vds            {Add-VDSwitchPhysicalNetworkAdapter, Add-VDSwitchVMHost, Export-VDPortGroup, Export-VDSwitch...}
Script     10.0.0.... VMware.VimAutomation.Vmc            {Connect-Vmc, Disconnect-Vmc, Get-VmcService, Connect-VmcServer...}
Script     10.0.0.... VMware.VimAutomation.vROps          {Connect-OMServer, Disconnect-OMServer, Get-OMAlert, Get-OMAlertDefinition...}
Script     6.5.1.7... VMware.VumAutomation                {Add-EntityBaseline, Copy-Patch, Get-Baseline, Get-Compliance...}
```

### Explanation

### *[Find-Module](https://docs.microsoft.com/en-us/powershell/module/powershellget/find-module?view=powershell-6)*

Finds modules from an online gallery that match specified criteria. By default, it refers to the [PowerShell Gallery](https://www.powershellgallery.com/). [Register-PSRepository](https://docs.microsoft.com/en-us/powershell/module/powershellget/register-psrepository?view=powershell-6) allows you to add additional galleries.

#### *-Name*

The name of the module you are looking for.

### *[Install-Module](https://docs.microsoft.com/en-us/powershell/module/powershellget/install-module?view=powershell-6)*

Downloads modules from an online gallery and installs them on the local computer. By default, it refers to the [PowerShell Gallery](https://www.powershellgallery.com/).

### *-Name*

Specify the exact names of the modules to install. Supports wildcard characters.

### *[Get-Module](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-module?view=powershell-6)*

Gets the modules that have been imported into the current session.

### *-Name*

Specify names or name patterns of modules. Supports wilcard characters.

### *-ListAvailable*

Gets all installed modules listed in [PSModulePath](https://docs.microsoft.com/en-us/powershell/developer/module/modifying-the-psmodulepath-installation-path) environment variable.

## Conclusion

Once you have installed PowerCLI as above, connect to your VMware environment using [Connect-VIServer](https://code.vmware.com/docs/6702/cmdlet-reference#/doc/Connect-VIServer.html). Once credentials have been passed, you are able to manage your VMware environment using PowerCLI.

Hope you're having a great day and this is of use.

Thanks, Tim.
