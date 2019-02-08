---
layout: default
title: "The Joy of Community"
date: 2019-02-08
---
# {{ page.title }}

## Introduction

In April 2018, I started this blog. I started it so that I could document some of the things I was interested in and also to share knowledge. I have been involved with PowerShell since 2009 and started to 'give back' to the community via [Stack Exchange](https://stackexchange.com/users/9500988/tim-haintz?tab=accounts) & [Microsoft TechNet](https://social.technet.microsoft.com/profile/tim%20haintz/) in late 2016. Helping out via the forums led me into writing this blog.

For the past 10 months, I have been writing and publishing posts, not 'realeasing' them publicly. On the 6th of February this year, I decided to use [Twitter](https://twitter.com/timhaintz/status/1092873004978122752) to announce my new blog post. What a great idea that was! Within an hour, I had feedback not just from the PowerShell community, but from the exact people that have unknowingly helped me out over the years from their own blogs, websites and articles. [SQLDBAwithbeard](https://twitter.com/sqldbawithbeard) & [Mike F Robbins](https://twitter.com/mikefrobbins) both provided valuable ideas.

The below scripts show the value of community and sharing. My original script is shown first. The *SQLDBAwithbeard* and *Mike F Robbins* suggestions are also shown.

### Script

#### Original Post Pester Code Block

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

#### [SQLDBAwithbeard suggestion Pester Code Block](https://twitter.com/sqldbawithbeard/status/1092885384772624384)

```powershell

```

#### [Mike F Robbins suggestion Pester Code Block](https://mikefrobbins.com/2016/12/09/loop-through-a-collection-of-items-with-the-pester-testcases-parameter-instead-of-using-a-foreach-loop/)

```powershell

```

### Results

#### When a service is off, the below failure is displayed

![Pester Multiple Services - Remote Fail](/assets/20190206/1-PesterMultipleServicesRemoteF.png)

#### When the services are all running, the below success is displayed

![Pester Multiple Services - Remote Pass](/assets/20190206/2-PesterMultipleServicesRemoteP.png)

## Explanation

## Conclusion

Hope you're having a great day and this is of use.

Thanks, Tim.
