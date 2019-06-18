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
      * Pin the resource to a specific zone
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
* *Authenticate access with Azure Active Directory*
  * Azure AD is all about web-based authentication standards such as OpenID and OAuth
  * A tenant is a dedicated, isolated instance of the Azure Active Directory service, owned and managed by an organisation
  * Azure AD tenants and subscriptions have a many-to-one trust relationship
    * A tenant can be associated with multiple Azure subscriptions
    * Every subscription is associated with only one tenant

[Core Cloud Services - Manage services with the Azure portal](https://docs.microsoft.com/en-gb/learn/modules/tour-azure-portal/)

* *Azure management options*
  * Tools used for day-to-day management and interaction:
    * Azure portal, GUI
    * Azure PowerShell and Azure Command-Line Interface (CLI) for automation- based interactions
    * Azure Cloud Shell for a web-based command-line interface
    * Azure mobile app for monitoring and managing resources from mobile device
  * Azure portal
    * Web based
    * Identify a service you're looking for
    * Get links for help
    * Deploy, manage and delete resources
    * Wizards and tooltips to guide you through complex admin tasks
    * Can customise the dashboard
    * Time consuming and error prone for complex tasks as there is no automation
  * Azure PowerShell
    * Install the Azure PowerShell module
    * Sign in using `Connect-AzureRMAccount`
    * Powerful was to automate and optimise workflow
  * Azure CLI
    * Cross-platform command-line program
      * Runs on:
        * Windows
        * Linux
        * macOS
    * Login using `az login`
  * Azure Cloud Shell
    * Browser-based scripting environment
    * Two shell environments:
      * Bash for Linux
      * PowerShell for Windows
    * Supports Azure CLI and Azure PowerShell CLI
    * Also has a suite of developer tools available such as:
      * .NET Core,Python, Go
      * code, vim, nano
      * git, maven, make
    * An Azure Storage Account is created when you connect
      * $HOME folder
      * Scripts or data kept is available across sessions
      * Each subscription has a unique storage account associated
  * Azure mobile app
    * Access, manage and monitor all Azure accounts and resources from iOS or Android
    * Check current status
    * Start, stop, and restart virtual macines
    * Use Azure Cloud Shell
  * Other options
    * Azure SDKs
    * REST APIs
* Navigate the portal
  * A *blade* is a slide-out panel containing the UI for a single level in a navigation sequence
    * Some blade options generate another blade
  * The Marketplace allows customers to find, try, purchase, and provision applications and services
  * The bell icon displays the *Notifications* pane
  * (>_) displays the *Cloud Shell*
  * The gear icon opens the *Portal settings*
  * The smiley face icon opens the *Send us feedback* blade
  * Question mark opens the *Help* blade
  * *Help + Support options* opens the main support area and is also where *New support request* can be requested.
  * *Book and Filter* icon shows the *Directory + subscription* blade
  * *Profile settings* are found on your name in the top right hand corner
    * Profile settings include:
    * Sign in with another account or sign out
    * View account profile, where you can change your password
    * Check permissions
    * View your bill
    * Update contact information
  * *Azure Advisor*
    * Free service built into Azure that provides recommendations on:
      * High availability
      * Security
      * Performance and
      * Cost
* *Exercise - Work with blades*
  * Recommend doing the hands on exercises in the sandbox environment
* *Exercise - Use the Azure portal*
  * Recommend doing the hands on exercises in the sandbox environment
* *Azure Portal dashboards*
  * A dashboard is a customisable collectin of UI tiles displayed in the Azure portal
  * You can add, remove, and position tiles to create the view you want
  * Dashboards can be created for roles, RBAC can then be used to control who has access to the dashboard
  * Stored as JSON files
    * Can be shared
    * Need a resource group to share the JSON
    * Need to grant permissions to the JSON file
  * Didn't realise the dashboard was so customisable
  * Lots of modifications can be made
    * Size
    * Location on page
    * You can take elements from child blades and put them on the dashboard
* *Exercise - Customize the dashboard*
  * Recommend doing the hands on exercises in the sandbox environment
* *Access public and private preview features*
  * Test beta and other pre-release features, products, services, software, and regions
  * Previews are not covered by customer support
  * Once evaluated and tested successfully, it becomes *General Availablilty (GA)*
  * Private and Public preview
  * [Preview Azure portal](https://preview.portal.azure.com/)
  * GA releases are available on the "What's New" link or [Azure Updates](https://azure.microsoft.com/en-gb/updates/)

[Core Cloud Services - Azure compute options](https://docs.microsoft.com/en-gb/learn/modules/intro-to-azure-compute/)

* *Essential Azure compute concepts*
  * On demand compute for:
    * multi-core procesors
    * supercomputers
      * via virtual machines and containers
  * Serverless computing
  * Pay only for as long as you're using them
  * Four common compute techniques
    * Virtual machines
    * Containers
    * Azure App Service
    * Serverless computing
* *Explore Azure Virtual Machines*
  * IaaS
  * Total control over the operating system (OS)
  * Ability to run custom software
  * An image is a template used to create a VM
  * Moving a physical server to the cloud "lift and shift"
  * Must update and maintain a VM through patching etc.
  * Scaling VMs in Azure
    * Availability sets
      * Logical grouping of two or more VMs
      * Planned maintenance avoids updating availability sets at the same time
        * VMs are put into different update domains
      * Unplanned maintenance
        * Automatically switch to a working physical server
          * VMs that share common hardware are in the same fault domain
      * Three fault domains that each have a server rack
      * Five logical update domains
      * No cost to an availability set, only pay for the VM
    * Virtual Machine Scale Sets
      * Identical, load balanced VMs
      * Routes between VMs
      * Centrally manage, configure, and update a large number of VMs in minutes
      * Can scale up or down in response to demand or a defined schedule
    * Azure Batch
      * Large-scale job scheduling and compute management
* *Explore Containers in Azure*
  * Containers are meant to be:
    * Lightweight
    * Created
    * Scaled out
    * Stopped dynamically
  * Run multiple isolated applications on a single VM host
  * Azure supports Docker containers
  * Manage containers in Azure using:
    * Azure Container Instances (ACI)
      * PaaS offering that allows you to upload your containers and execute them directly
    * Azure Kubernetes Service (AKS)
      * Complete orchestration service for containers with distributed architectures
  * Containers are often used to create solutions using microservice architecture
    * This enables solutions to be broken down into smaller, independent pieces
* *Explore Azure App Service*
  * Enables you to build and host:
    * Web apps
    * background jobs
    * Mobile backends
    * RESTful APIs
  * PaaS
  * Types of web apps
    * Web apps
      * Window or Linux
      * ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP or Python
    * API Apps
      * Full Swagger support, and the ability to package and publish your API in the Azure Marketplace
    * WebJobs
      * Run a program (.exe, Java, PHP, Python or Node.js) or script (.cmd, .bat, PowerShell, or Bash)
    * Mobile Apps
      * Build a back-end for iOS and Android apps
      * Store mobile app data in a cloud-based SQL database
      * Authenticate customers agains common social providers
      * Send push notifications
      * Execute custom back-end logic  in C# or Node.js
* *Explore Serverless computing in Azure*
  * Azure takes care of managing teh server infrastructure and allocation/dealloation of resources based on demand
  * Scaling and performance are handled automatically
  * Event driven
  * Azure functions
    * Execute code based on an event
    * Stateless
    * Stateful (Durable Functions)
    * Can run locally or in cloud
  * Azure Logic Apps
    * Execute workflows built from predefined logic blocks
    * Persisted as JSON
    * GUI driven
      * From the Azure Portal
      * Visual Studio
    * Runs only in cloud
  * An orchestration is a collection of functions or steps, that are executed to accomplish a complex task


Hope you're having a great day and this is of use.

Thanks, Tim.
