---
layout: default
title: "Certification time?"
date: 2019-06-11
---
# {{ page.title }}

The first series of online training is [Cloud Concepts - Principals of cloud computing](https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/index). This is a fundemental overview of Azure. It is used as base knowledge for future concepts.

The second series of online training is [Core Cloud Services - Introduction to Azure](https://docs.microsoft.com/en-us/learn/modules/welcome-to-azure/index). This is more hands on and allows you to create a virtual machine using [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).

[Core Cloud Services - Azure architecture and service guarantees](https://docs.microsoft.com/en-us/learn/modules/explore-azure-infrastructure/index) discusses:

* *Datacentres and Regions in Azure*
  * Regions are networked together with a low-latency network.
    * Contains at least one, but potentially multiple datacentres.
    * Some services are only available in certain regions.
    * Global Azure services are Microsoft Azure Active Directory, Microsoft Azure Traffic Manager, and Azure DNS.
* *Geographies*
  * Are fault-tolerant to withstand complete region failure
  * Broken up into the following areas:
    * Americas
    * Europe
    * Asia Pacific
    * Middle East and Africa
  * Each region belongs to a single geography
* *Availablility Zones*
  * Are physically separate datacentres within an Azure region
  * Made up of one or more datacentres
  * Connected through high-speed, private fiber-optic networks
  * Used to build high-availability into applications
  * Primarily used for VMs, managed disks, load balancers, and SQL databases
  * Two categories:
    * Zonal services
      * Ping the resource to a specific zone
    * Zone-redundant services
      * Platform replicates automatically across zones
* *Region Pairs*
  * Each Azure region is paired with another region within the same geography at least 300 miles away
  * Reduces the likelihood of interruptions due to events such as natural disasters
  * Used for reliable services and data redundancy
  * Planned Azure updates are rolled out to paired regions one region at a time to minimise downtime and risk
* *Service Level Agreements for Azure*
  * SLAs for individual Azure products and services
  * Three key characteristics of SLAs for Azure products and services:
    1. Performance Targets
    2. Uptime and Connectvity Guarantees
    3. Service Credits

* *Composing SLAs across services*
  * Composite SLA is the name used when multiple SLAs are combined
* *Improve your app reliablity*
  * Know your app workload requirements
    * Resiliency
      * Ability of a system to recover from failures and continue to function
      * High availability and disaster recovery are two crucial components
  * Cost and complexity vs. high availability
    * As solutions grow in complexity, more services depend on each other
    * As you increase availability, you also increase the cost and complexity of the solution

[Create an Azure account](https://docs.microsoft.com/en-gb/learn/modules/create-an-azure-account/)

* *Azure accounts and subscriptions*
  * Account
    * Associated with one or more subscriptions
  * Subscription
    * Logical container used to provision resources
    * Most commonly used subscriptions are:
      * Free
      * Pay-As-You-Go
      * Enterprise Agreement
      * Student
    * Access control and billing occur at the subscription level
  * Authenticate access with Azure Active Directory
    *



Hope you're having a great day and this is of use.

Thanks, Tim.
