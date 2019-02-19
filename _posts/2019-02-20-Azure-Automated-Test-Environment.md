---
layout: default
title: "Azure Automated Test Environment"
date: 2019-02-20
---
# {{ page.title }}

## Introduction

How would you like to enter a username/password and a fully built Active Directory and Certificate Authority test environment deploys in Azure? [Azure Automated Test Environment](https://github.com/timhaintz/aate) (AATE) does just that.

With the adoption of Infrastructure as Code, I noticed there wasn't a base level of automation to setup an environment from scratch. A true green fields deployment. [Desired State Configuration](https://docs.microsoft.com/en-us/powershell/dsc/overview/overview) (DSC) assumes you already have an environement setup. [Azure Resource Manager Templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) (ARM Templates) assume you have an environment to deploy to. The environment needs a subscription, resource group, storage, networking, credential storage etc.

I created my first Open Source project to solve this problem. Once you have an Azure account, AATE asks you to enter a username and password. AATE then deploys and builds everything you need as shown in the screen shot below.

![All resources](/assets/20190220/allResources.png)

### History

I originally wrote all of the DSC sections of AATE using [Hyper-V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/). Managing the base OS creation using the [Microsoft Deployment Toolkit](https://www.microsoft.com/en-au/download/details.aspx?id=54259) was time consuming. [Johan Arwidmark](https://deploymentresearch.com/) has some great posts about how to deploy images. I used a lot of Johan's blogs and videos to get my Hyper-V environment up and running.

I realised that using Hyper-V wasn't as easily sharable as using Azure. Base OS images were needed to be built locally before being able to deploy the DSC components. I embarked on re-factoring my Hyper-V scripts to deploy in Azure, that's where AATE was born.

Throughout the journey of building AATE, I started to help out with some [DscResources](https://github.com/PowerShell/DscResources). A massive thank you to [Dan Scott-Raynsford](https://twitter.com/dscottraynsford) for being so welcoming into the PowerShell and DSC space. He works tirelessly and was really helpful getting me started contributing to the community. The DSC changes enabled me to change the drive letter on the Domain Controller to E drive. Until this update, there was some user intervention required for the build. I have left the user intervention help section commented out as a reminder and thank you. [Issue #140](https://github.com/PowerShell/StorageDsc/issues/140) has the solution and explanation.

### Usage

I use AATE as a test environment that I build and destroy as I choose. It is a great way to test out and experiment in Azure. If you have a [Visual Studio Subscription](https://visualstudio.microsoft.com/subscriptions/) previously an MSDN subscription, you receive [Monthly Azure credit](https://azure.microsoft.com/en-au/pricing/member-offers/credit-for-visual-studio-subscribers/). You can also setup a [Free Azure Account](https://azure.microsoft.com/en-au/free/). Once you have finished testing you just destroy the environment and you no longer have usage charges.

I have written AATE to use the unique Azure SubscriptionID to generate public DNS in the [ARMTemplate](https://github.com/timhaintz/aate/blob/master/AzureRM/ARMTemplate.json) file.
`"domainNameLabel": "[concat(parameters('dnsLabelPrefix'), substring(uniqueString(subscription().subscriptionId),0,6))]"`.
There shouldn't be any overlap with public DNS usage.

If you deploy AATE, you may notice that the Active Directory domain name is timhaintz.com. Why use my own name? I bought the .com domain name so that no one else could use it publicly. I know it will never have anything public on it as I use timhaintz.com.au. You can change the domain name in AATE if you prefer. The [Regular Expression](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_regular_expressions?view=powershell-6) for .com was also easier than catering for all of the other possible combinations. If you do choose to rename, you will need to keep it as .com.

If you are looking to create complex labs, please see [AutomatedLab](https://github.com/AutomatedLab/AutomatedLab), it is a great project. I didn't know about AutomatedLab when I started what would become AATE.

## Conclusion and Next Steps

Please feel free to provide feedback. Happy to accept Issues and Pull Requests. Also happy for it to be expanded upon to peform further tasks. Something I would like to do in the future is also deploy a Linux server and use DSC to deploy a webserver and simple webpage using a certificate generated from the CA. The idea is for it to remain simple to consume for end users. Enter a username and password then explore and experiment in Azure.

Again, thank you to [Dan Scott-Raynsford](https://twitter.com/dscottraynsford) for helping me out and being so welcoming. That started my community contributions and has led me down the path of writing this blog. Thank you also to everyone that wrote the posts on [URLs used to build initial environment](https://github.com/timhaintz/aate#urls-used-to-build-initial-environment).

Hope you're having a great day and this is of use.

Thanks, Tim.
