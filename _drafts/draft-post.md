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

[Core Cloud Services - Azure data storage options](https://docs.microsoft.com/en-gb/learn/modules/intro-to-data-in-azure/)

* *Benefits of using Azure to store data*
  * Automated backup and recovery
  * Replication across the globe
  * Support for data analytics
  * Encryption capabilities
  * Multiple data types
  * Data storage in virtual disks
  * Storage tiers
  * Types of data:
    * Structured data (relational data)
    * Semi-structured data (non-relational or NoSQL)
    * Unstructured data
* *How Azure data storage can meet your business to storage needs*
  * Azure SQL Database
    * DaaS
    * Azure Database Migration Service to move on-prem to cloud
      * Uses Microsoft Data Migration Assistant
    * Just change connection sting in Apps once migrated
  * Azure Cosmos DB
    * Globally distributed database service
    * Schema-less data
    * Supports Always On applications
  * Azure Blob storage
    * Unstructured
      * No restrictions on the kinds of data it can hold
    * Highly scalable
    * Reached from anywhere with an internet connection
    * Store up to 8TB of data for virtual machines
  * Azure Data Lake Storage Gen2
    * Scalability and cost benefits of object storage
    * Reliability and performance of the Big Data file system capabilities
    * Cleanses, enriches, annotates and schematises data
    * Ingest -> Prepare -> Store -> Analyse
  * Azure Files
    * Fully managed files shares
    * Accessed via Server Message Block (SMB)
    * Mounted concurrently by cloud or on-premises by Windows, Linux and macOS
    * SMB ensures data is encrypted at rest and in transit
  * Azure Queue
    * Service for storing large numbers of messages
    * Asynchronous message queueing for communication between application components
    * One or more sender components
    * One or more receiver components
  * Disk Storage
    * Allows data to be persistently stored and accessed from an attached virtual hard disk
    * Managed and unmanaged disks
  * Storage tiers for blob storage:
    * Hot storage tier - accessed frequently
    * Cool storage tier - accessed infrequently stored for at least 30 days
    * Archive storage tier - accessed rarely stored for at least 180 days with flexible latency requirements
  * Encryption and replication for storage services
    * Azure Storage Service Encyption (SSE)
      * Data at rest
      * Encypts data before storing it
      * Decypts data before retrieving it
      * Encyption/decryption transparent to the user
    * Client-side encryption
      * Data already encrypted by client libraries
  * Replication for storage availability
    * Replication type is setup when you create a storage account
    * Regional and geographic replication
* *Comparison between Azure data storage and on-premises storage*
  * Cost effectiveness
    * Azure is pay-as-you-go pricing
    * Scalable
  * Reliability
  * Storage types
  *Agility

[Core Cloud Services - Azure networking options](https://docs.microsoft.com/en-gb/learn/modules/intro-to-azure-networking/)

* *Deploy your site to Azure*
  * Benefits of Loosely Coupled Architectures
    * N-tier architecture
      * Divides an application into two or more logical tiers
      * A higher tier can access services in a lower tier, but a lower tier should never access a higher tier
      * Tiers are designed to be reusable and replacable
  * What's a virtual network?
    * Logically isolated network on Azure
    * Scoped to a single region
    * Multiple virtual networks from different regions can be connected together using virtual network peering
    * Can be segmented into one or more subnets
  * What's a network security group (NSG)?
    * Allows or denies inbound network traffic
* *Scale with Azure Load Balancer*
  * What are availability and high availability?
    * Availability refers to how long your service is up and running without interruption
    * Five nines availability mean service is guaranteed to be running 99.999% of the time
  * What is resiliency?
    * Resiliency refers to a system's ability to stay operational during abnormal conditions
  * What is a load balancer?
    * A load balancer distributes traffic evenly among each system in a pool
    * Can help achieve both high availability and resiliency
  * What is Azure Load Balancer?
    * Load balancer service that Microsoft provides that helps take care of maintenance for you
    * Provides low latency and high throughput
    * Scales up to millions of flows for all TCP and UDP applications
  * Azure Application Gateway
    * HTTP(S) load balancer that uses Azure Load Balancer at the TCP layer
    * Application layer (OSI layer 7) load balancing
    * Cookie affinity
    * SSL termination
    * Web application firewall
    * URL rule-based routes
    * Rewrite HTTP headers
  * What is a Content Delivery Network?
    * Distributed network of servers that can efficiently deliver web content to users
    * Get content to users in their local region to minimise latency
    * Cache content at strategically placed physical nodes across the world
  * What about DNS (Domain Name System)?
    * Is a way to map user-friendly names to their IP addresses
    * Can host using Azure DNS
  * Reduce latency with Azure Traffic Manager
    * What is network latency?
      * Time is takes for data to travel over the network
        * Typically measured in milliseconds
      * Bandwidth refers to the amount of data that can fit on the connection
    * Use Traffic Manager to route users to the closest endpoint
      * Uses the DNS server that's closest to the user to direct user traffic to a globally distributed endpoint
      * Doesn't see the traffic, rather it redirects the client web browser to the preferred endpoint

[Security, responsibility and trust in Azure](https://docs.microsoft.com/en-gb/learn/modules/intro-to-security-in-azure/)

* *Cloud security is a shared responsibility*
  * Shared security responsibility with Azure
    * IaaS leverages the lowest-level service
      * Need to patch and manage the security of the environment
    * PaaS outsources a lot of security concerns
      * Microsoft looks after the OS and most foundational software
      * Everything is updated with the latest patches
    * SaaS code is controlled by the vendor but configured to be used by the customer
  * A layered approach to security
    * Defence in depth is a layered approach to security
      * Employs a series of mechanisms to slow the advance of an attack
      * Each layer provides protection
    * Layers are:
      * Data
        * Responsibility of the customer to secure their data
      * Application
        * Ensure applications are secure and free of vulnerabilities
      * Compute
        * Patch systems and make servers secure
      * Networking
        * Limit communication between resources
        * Deny by default
      * Perimeter
        * Use DDos protection
        * Firewalls
      * Identity and access
        * Use single sign on and MFA
        * Audit events and changes
      * Physical security
        * Provide physical safeguards
  * Get tips from Azure Security Center
    * Provides security recommendations
    * Monitors security settings
    * Perform automatic security assessments
    * Use machine learning to detect and block malware
    * Analyse and identify potential inbound attacks
    * Provide just-in-time access control
    * Part of the Center for Internet Security (CIS) recommendations
    * Free tier
    * Standard tier
    * Incident response
      * Detect
      * Assess
      * Diagnose
    * Use recommendations to enhance security
      * Security policy defines the set of controls that are recommended for resources with the subscription or Resource Group
      * Creates recommendations based on the controls set in the policy
    * Identity and access
      * Authentication (AuthN)
        * The process of establishing the identity of a person or service looking to access resources
      * Authorization (AuthZ)
        * The process of establishing what level of access an authenticated person or service has
  * What is Azure Active Directory (Azure AD)?
    * Cloud-based identity service
    * Built in support to synchronise with exsiting on-premises Active Directory or can be used stand alone
    * Azure AD provides:
      * Authentication
        * SSPR
        * MFA
      * Single-Sign-On (SSO)
      * Application management
        * Azure AD Application Proxy
      * Business to business (B2B) identity services
        * Manage guest users and external partners
      * Device Management
    * Providing identities to services
      * Service principals
        * A principal is an identity acting with certain roles or claims
        * A Service Principal is an identity that is used by a service or application
      * Managed identities for Azure services
        * When you create a managed identity for a service, you are creating an account on the Azure AD tenant
        * Azure infrastructure will automatically take care of authenticating the service and managing the account
    * Role-based access control
      * Identities are mapped to roles directly or through group membership
      * Roles assigned at a higher scope, like an entire subscription, are inherited by child scopes, like service instances
    * Privileged Identity Management (PIM)
      * Provides oversite of:
        * Role assignments
        * Self-service
        * Just-In-Time role activation
        * Azure AD and Azure resource access reviews
  * Encryption
    * Encyption is the process of making data unreadable and unusable to unauthorised viewers
    * Decryption requires the use of a secret key
    * Two types of encryption:
      * Symmetric
        * Uses the same key to encrypt and decrypt
      * Asymmetric
        * Public key and private key pair
        * Either key can encrypt, only one key can decrypt
        * Used in Trasnport Layer Security (TLS) and data signing
    * Encryption at rest
      * Encrypting data at rest means if a hard drive is stolen, it is very, very difficult to read the actual data
    * Encryption in transit
      * HTTPS is an example of application layer in transit
      * VPN is an example of a secure channel at the network layer
    * Encryption on Azure
      * Azure Storage Service Encryption
        * Azure storage platform
          * Automatically encrypts your data before persisting it to Azure Managed disks
          * Encryption, decryption, and key mangegement in Storage Serice Encryption is transparent to applications and services
      * Encrypt virtual machine disks
        * Azure Disk Encryption, BitLocker for Windows, dm-crypt for Linux
          * Integrated with Azure Key Vault
      * Encrypt databases
        * Transparent data encryption (TDE) protects Azure SQL Datbase and Azure Data Warehouse
          * Real-time encryption and decryption of database and transaction logs
          * On by default for newly deployed Azure SQL Database instances
      * Encrypt secrets
        * Azure Key Vault
          * Centralised cloud service for storing application secrets
  * Protect your network
    * A layered approach to network security
      * Ensure internet facing services are locked down to only allow inbound and outbound communication where necessary
      * Restrict the ports and protocols required
    * What is a Firewall?
      * Firewall rules, generally speaking, also include specific network protocol and port information
      * Azure Firewall is a managed, cloud-based, network security service
        * Fully stateful firewall as a service
      * Azure Application Gateway is a load balancer that includes a Web Application Firewall (WAF)
      * Network virtual applicances (NVAs) are ideal optoins for non-HTTP services or advanced configurations
    * Stopping Distributed Denial of Service (DDos) attacks - Azure DDos Protection Service
      * DDos attacks try to overwhelm a network resource by sending so many requests that the resource becomes slow or unresponsive
      * Basic tier is automatically enabled
      * Standard tier provides additional mitigation capabilities
        * Volumetric attacks
        * Protocol attackes
        * Resource (application) layer attacks
    * Controlling the traffic inside your virtual network
      * Virtual network security
        * NSGs are critical to restrict unnecessary communication
      * Network integration
        * VPN
        * Azure Express Route
          * Use a private circuit rather than the public internet
  * Protect your shared documents
    * Microsoft Azure Information Protection (MSIP or sometimes AIP) helps classify and optionally protect documents
      * Labels can be applied automatically based on rules and conditions
  * Azure Advanced Threat Protection (ATP)
    * Cloud-based security solutions that:
      * Identifies
      * Detects
      * Helps investigate:
        * Advanced threats
        * Compromised identities
        * Malicious insider actions
    * Azure ATP portal
    * Azure ATP Sensor
      * Installed directly on domain controllers
    * Azure ATP cloud service

[Apply and monitor infrastructure standards with Azure Policy](https://docs.microsoft.com/en-gb/learn/modules/intro-to-governance/)

* *Define IT compliance with Azure Policy*
  * Azure Policy is an Azure service used to:
    * Define, Assign & Manage standards for resources in your environment
    * Prevent disallowed resources
    * Scan for non-compliance
    * Able to prohibit certain resources, for example, VMs can have a maximum of 4 CPUs
      * Stock Keeping Units (SKUs)
    * Can integrate with Azure DevOps
  * Creating a policy
    * Use a policy definition
    * To apply a policy:
      * Create a policy definition
      * Assign a definition to a scope of resources
      * View policy evaluation results
  * What is a policy definition?
    * A policy definition expresses what to evaluate and what action to take
    * Represented as a JSON file
  * Assign a definition to a scope of resources
    * A policy assignment is a policy definition that has been assigned to take place within a specific scope
    * Policy assignments are inherited by all child resources
  * Policy effects
    * Each policy definition in Azure Policy has a single effect
    * Effects determine what happens when the associated policy rule is matched
    * The policy effects are:
      * Deny
      * Disabled
      * Append
      * Audit, AuditIfNotExists
      * DeployIfNotExists
  * View policy evaluation results
    * Azure Policy can allow a resource to be created even if it doesn't pass validation
    * It can trigger an audit event which can be viewed in the Azure Policy portal
* *Organize policy with initiatives*
  * Initiatives work alongside policies in Azure Policy
  * An initiative definition is a set or group of policy definitions
  * An initiative assignment is an initiative definition assigned to a specific scope
* *Enterprise governance management*
  * Access management occurs at the Azure subscription level
  * Azure Management Groups are containers for managing access, policies, and compliance across multiple Azure subscriptions
  * All subscriptions within a management group automatically inherit the conditoins applied to the management group
  * Management groups can be used to provide user access to multi subscriptions
    * Adding the subscriptions under the management group, one RBAC group can be created to manage all subscriptions
* *Define standard resources with Azure Blueprints*
  * Azure Blueprints help with auditing, traceability and compliance
  * Azure Blueprints is a declarative way to orchestrate the deployment of resource templates and other artefacts such as:
    * Role assignments
    * Policy assignments
    * Azure Resource Manager templates
    * Resource groups
  * Implementing Azure Blueprints:
    * Create an Azure Blueprint
    * Assign the blueprint
    * Track the blueprint assignment
* *Explore your service compliance with Compliance Manager*
  * What is the Microsoft Trus Center?
    * Trust Center is a website resource containing information about how Microsoft implements and supports:
      * Security
      * Privacy
      * Compliance
      * Transparency
  * What is the Service Trust Portal (STP)?
    * Microsoft public site for publishing audit reports and other compliance-related information for Microsoft's cloud services
  * Compliance Manager
    * Compliance Manager is a workflow-based risk assessment dashboard within the Trust Portal
* *Monitor your service health*
  * Azure Monitor
    * Data sources
      * Application monitoring data
      * Guest OS monitoring data
      * Azure resource monitoring data
      * Azure subscription monitoring data
      * Azure tenant monitoring data
    * Application insights
      * Service that monitors the availability, performance and usage of web applications
      * Leverages Log Analytics
    * Azure Monitor for containers
      * Service designed to monitor the performance of containers
    * Azure Monitor for VMs
      * Service that monitors VMs at scale
  * Azure Service Health
    * Suite of experiences that provide personalised guidance and support when issues with Azure services affect you
    * Azure Status
      * Provides a global view of the health state of Azure services
    * Service Health
      * Customisable dashboard that track the state of your Azure services
    * Resource Health
      * Helps diagnose and obtain support when an Azure service issues affects your resources
      * Personalised dashboard of your resources' health

[Control and organise Azure resources with Azure Resource Manager](https://docs.microsoft.com/en-gb/learn/modules/control-and-organize-with-azure-resource-manager/)




Hope you're having a great day and this is of use.

Thanks, Tim.
