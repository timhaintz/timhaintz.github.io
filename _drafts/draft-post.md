---
layout: default
title: "The Power of Community"
date: 2019-02-10
---
# {{ page.title }}

## Introduction

I started blogging in April 2018 to document things I was interested in and to share knowledge. I have been using PowerShell since 2009 and started to *give back* to the community via [Stack Exchange](https://stackexchange.com/users/9500988/tim-haintz?tab=accounts) & [Microsoft TechNet](https://social.technet.microsoft.com/profile/tim%20haintz/) in late 2016. Helping via the forums led me to writing this blog.

For the past 10 months, I have been writing and publishing posts, not *realeasing* them publicly. On the 6th of February this year, I decided to use my newly created Twitter account to announce my [new blog post](https://twitter.com/timhaintz/status/1092873004978122752). What a great experience that was! Within an hour, I had feedback not just from the PowerShell community, but from the exact people that have unknowingly helped me out over the years from their own blogs, websites and articles. [SQLDBAwithbeard](https://twitter.com/sqldbawithbeard) & [Mike F Robbins](https://twitter.com/mikefrobbins) both provided valuable feedback to my original Pester script.

The below scripts show the value of community and sharing. My original script is shown first. The *SQLDBAwithbeard* and *Mike F Robbins* suggestions are shown after.

### Script

### Original Post - Pester Code Block

```powershell
# Services we want to test for
$services = 'bthserv','WinRM'
# Loop through the services
Describe "Testing critical services on ca1" {
    $services.ForEach{
        Context "Testing $($_)" {
            It "The $($_) service should be running" {
                (Invoke-Command -ComputerName ca1 -ScriptBlock {param($_) Get-Service -ServiceName $_} -ArgumentList $_ ).status | Should be 'Running'
            }
        }
    }
}
```

### Original Results

#### When a service is off, the below failure is displayed

![Pester Multiple Services - Remote Fail](/assets/20190210/1-PesterMultipleServicesRemoteF.png)

#### When the services are all running, the below success is displayed

![Pester Multiple Services - Remote Pass](/assets/20190210/2-PesterMultipleServicesRemoteP.png)

### [SQLDBAwithbeard suggestion - Pester Code Block](https://twitter.com/sqldbawithbeard/status/1092885384772624384)

Please note, the below syntax `Should -Be` requires [Pester v4](https://github.com/pester/Pester/wiki/Should).

```powershell
# Services we want to test for
$services = Get-Service 'bthserv','WinRM' -Computername ca1
# Loop through the services
Describe "Testing critical services on ca1" {
    $services.ForEach{
    It " $($PsItem.Name) should be running" {
        $Psitem.Status | Should -Be 'Running' -Because 'these are critical services on this server.'
        }
    }
}
```

### SQLDBAwithBeard Results

#### When a service is off, the below failure is displayed

![Pester Multiple Services - SQLDBAwithBeard - Remote Fail](/assets/20190210/1-PesterMultipleServicesRemoteSQLDBAF.png)

#### When the services are all running, the below success is displayed

![Pester Multiple Services - SQLDBAwithBeard - Remote Pass](/assets/20190210/2-PesterMultipleServicesRemoteSQLDBAP.png)

### [Mike F Robbins suggestion - Pester Code Block](https://mikefrobbins.com/2016/12/09/loop-through-a-collection-of-items-with-the-pester-testcases-parameter-instead-of-using-a-foreach-loop/)

```powershell
Describe 'Testing critical services on ca1' {
    $services = @{service = 'bthserv'}, @{service = 'WinRM'}
    It "The <service> Service on ca1 Should Be Running" -TestCases $services {
        param($service)
        (Get-Service -ComputerName ca1 -Name $service).Status |
        Should Be 'Running'
    }
}
```

### Mike F Robbins Results

#### When a service is off, the below failure is displayed

![Pester Multiple Services - Mike F Robbins - Remote Fail](/assets/20190210/1-PesterMultipleServicesRemoteMikeFF.png)

#### When the services are all running, the below success is displayed

![Pester Multiple Services - Mike F Robbins - Remote Pass](/assets/20190210/2-PesterMultipleServicesRemoteMikeFP.png)

## Conclusion

As you can see from the results of the tests, my original method of testing was very inefficient. *SQLDBAwithBeard's* method shows to be the most efficient with *Mike F Robbins'* method of using `-TestCases` being more Pester-Purist in the words of [Matt Hitchcock](https://twitter.com/hitchysg_MSFT).

What has releasing my blog to the community shown me? The PowerShell and Pester community are awesome and very helpful. There are also multiple ways to get to the same outcome and it is great to learn new methods.

Thank you to everyone in the PowerShell community. I hope to keep sharing and any feedback I receive, I will try and pass on.

Keep learning and practicing Kaizen.

Hope you're having a great day and this is of use.

Thanks, Tim.
