# az-104-interviewquestions

Azure AD
-----------
User, Group, Service Principal and Managed Identity.

User Assigned Managed Identity and System Assigned Managed Identity.

Identity Types
-Cloud Identities
-Guest Identities
-Directory Synced Users

Group Types
-Security Groups
-Microsoft 365 Groups

Assignment Membership Types like Assigned, Dynamic User. Dynamic Device(Security Group Only).

Azure AD Join

Azure AD Connect

SSPR

Management Group

Subscription

6 levels of Nested Groups excluding the Root Group.

Role Based Access Control
Who - Security Principal - User
What - Role Definition - Reader
Where - Scope - Resource Group

Who + What + Where = Role Assignment upto max 2000 in a subscription.

Principle of Least Privilege.

Built-in roles vs Custom Roles
Built-in
-Owner - Full access + Grant others access
-Contributor - Read/Write - Grant others access
-Reader - Read Only
-User Access Admin

Custom
Each Directory can have upto 5000 custom roles

Can inherited role assignments be removed? No

Azure RBAC vs Azure AD roles

Azure Tags
How can i get all the resources created by IT team.

-Adding Metadata like Cost Center, Environment, Department
-Logical Grouping
-Name-Value pair
-Cost Management

Tag Name limit 512
Tag Value limit 256
Max Tags limit 50

Are Azure Tags inheritable by default?
How can you make the Azure Tags inheritable from Resource Group to Resource. It can be done by using Azure policy "Inherit a tag from the resource group if missing".

Resource Locks
---------------
Avoid Accidental Changes

Inheritance from higher scope to lower.

Read-Only Locks - cannot be modified Cannot Delete VM nor restart or stop it.
Delete Locks - can be modified but prevents deletion for accidental changes. Cannot delete VM but can stop or restart it.

Cost Savings
-Azure Reserved instances for 1 to 3yrs
-Azure Hybrid Usage Benefits like Windows and SQL server licenses cost effective than Pay-as-you-go 
-Credits from Visual Studio, MPN
-Regions but take care of compliance

I want to generate a report of cost on a particular date of the month. It should be automated. Use Cost Exports.

Azure Policy
------------

Define Organizational standards and identify non-compliant resources.

Azure Policy can be applied at Management Group, Subscription and Resource Group but not at the resource level. To exclude a resource from Azure Policy enforcement, use the exclusion feature.

Steps in Azure Policy creation
-Definition
-Scope
-Assignment
-Compliance

Azure Policy - Use Cases

-Allowed Resource Types
-Allowed VM SKUs
-Locations
-Allowed Resource Group Location
-Require Tags
-Inherit Tags


Initiative
Chaining policy definitions so that they can be assigned as a single item and the compliance can be evaluated.

Use Case - Initiative
Restrict user from creating a resource type of Cosmos DB + Other resources should have a Tag named a Cost Center + Allowed location is East Us and West Us + Azure Backup is enabled for VMs + Allowed VM SKUs like BS, DSv2.

Azure Policy takes precedence over Owner roles as well. Owner roles cannot bypass Azure Policy.

Azure VNET
----------
Representation of Cloud Network. Logical representation of your network on Cloud.

Every VNET instance in Azure is private and dedicated.

With the help of VNETs, we can extend our communication to on-premises datacentres and other cloud providers securely.

Azure Region represents a set of datacentres which are part of different availability zones. Each Azure Region can contain one or more VNETs.

Each VNET we create should have an address space. We can use public or private adresses for your address space. Thumb rule, do not let your address space overlap other VNET or on-premise address space. Whenever we create a resource in the VNET, the IP address is given from address space.

Subnets helps us to segment our VNET address space to smaller subnetworks.

DDOS and Firewall can be enabled during VNET creation.

IP Addresses are needed for communication.

Private IP addresses
--------------------
are used within Azure Virtual Network, Hybrid scenarios such as VPN Gateway and Express Route Connections.

Private IP address have allocation methods: 
Static - Setting Static IP addresses for Domain Controllers, Web Servers and DNS Servers. Load Balancers and Application Gateways. Servers ip address remains same even after restart.

Dynamic - Is the default option. Server ip changes post server restart. Router will have Dynamic IP adresses.

DHCP:- Dynamic Host Configuration Platform

Public IP addresses
-------------------
are used for communicating with the internet and azure public facing services

Static and Dynamic Allocation types

SKUs:- Stock Keeping Units - Basic and Standard

               Basic                                                       Standard
 -----------------------------------------------------------------------------------              
IP Allocation  Dynamic/Static                                              Static
Security       Open                                                        Closed
Resources      VM NIC, VPN Gateways, Public LB and App Gateways            VM NIC, Public LB and App Gateways
Redundancy     No Redundancy                                               Zone Redundant

Azure reserves 5 ip addresses in a subnet, 1 for network address, 1 for default gateway, 2 for DNS ip addresses and 1 for broadcast.

User Defined Routes
-------------------
UDR allows you to override the default communication allowed between multiple VMs in same VNET but different subnets using Route Table passing the traffic through NVA like DMZ VM.

System Routes allows
--------------------
Communication between VMs in the same subnet
Communication between VMS in different subnet within same VNET
Communication from VM to the internet
Communication via Site-to-Site and ExpressRoute connection while using VPN Gateways.

NOTE:- Communication from internet to VM is locked by default due to NSG.
NOTE:- In other Cloud Providers, we need NAT Gateways or Internet Gateways for VM to communicate with internet.

We can override the System Route which by default allows communication from the FrontEnd Subnet1 to DB Subnet2 within the same VNET by using Route Table.

Service Endpoints
--------------------
By Default VM can access the Azure Storage Account. As part of the Storage Firewall the Public ip of the VM will be whitelisted. This will work when the Public IP of the VM is static. However when the IP is dynamic, then in that case we cannot configure the Storage Firewall with Dynamic Public IPs. In such a case, we can use Service Endpoints wherein the VNET ie. the private ip of the VM will become the source IP for the Storage Account firewall as the VNET IP will be whitelisted on the Storage Account Firewall.
Source IP is private but destination IP is Public.
Extends the VNET of the source Azure Service to the Destination Service by setting up VNET based on Source IP.
Operates at the Service Level.

Benefits
Access Azure Services with better security. No need for the Public IP of the VM or Azure resource.
Leverages Microsoft Backbone network.
Ease of setup and management. Simply provide VNET and no need to maintain public IP.


Private Endpoint
----------------
Source IP is Private and also the Destination IP.
Its a 1-1 service.
Operates at the Service Instance level ie. resource level.

**NOTE:- Private Endpoint must be in the same region as VNET, but can be in diff region from the private link resource that you are connecting to**.

Brings the Destination Service into the Source VNET by allocating the Private IP to the Destination Service.

Benefits
Connects to Azure Services via Private Connection.
Seamless integration with On-Premise and Peered Networks.
Eliminate risk of data exfiltration.
Direct availability in Azure VNETs.

dig dns tool to get infor on the host
dig <<hostname>>

Certainly! Let's start with an overview of Azure Service Endpoint and Azure Private Endpoint.

**Azure Service Endpoint:**

Azure Service Endpoint is a feature that allows you to extend your virtual network to Azure services over a direct and optimized route. This helps secure your critical Azure service resources to your virtual network, improving security and network performance. When you enable a service endpoint for a subnet, the traffic to the Azure service of that type gets a direct route to the service over the Azure backbone network.

**Example Use Case:**

Imagine you have an Azure SQL Database that you want to connect to from within your Azure Virtual Network. Without a service endpoint, the traffic would have to go over the internet. By configuring a service endpoint for Azure SQL Database in your virtual network subnet, the traffic takes a more direct and secure route over the Azure backbone, enhancing security and performance.

**Azure Private Endpoint:**

Azure Private Endpoint is a network interface that connects you privately and securely to a service powered by Azure Private Link. It uses a private IP address from your virtual network, effectively bringing the Azure service into your virtual network. This provides a more secure connection to the service, as the traffic does not go over the internet.

**Example Use Case:**

Let's say you're using Azure Storage and want to ensure that your data transfers between your virtual network and the storage account happen securely and privately. By creating a private endpoint for Azure Storage in your virtual network, you get a private IP address that can be used to connect to the storage account. This way, the data transfer occurs over the Azure backbone network, avoiding exposure to the public internet.

**Summary:**

In essence, Azure Service Endpoint enhances the network path to Azure services, optimizing traffic flow and security within the Azure backbone. On the other hand, Azure Private Endpoint brings the Azure service directly into your virtual network, providing a more secure and private connection by utilizing a private IP address.

Both Azure Service Endpoint and Azure Private Endpoint are tools to enhance the security and performance of your Azure services within your virtual network, but they achieve this in slightly different ways.

You bring up a valid point, and managing multiple individual endpoints for various Azure services can indeed become cumbersome. To address this challenge, Azure offers a solution called **Azure Private Link Service**.

**Azure Private Link Service:**

Azure Private Link Service simplifies the process of connecting to multiple Azure services within your virtual network. Instead of creating individual endpoints for each service, you can create a Private Link Service that acts as a common entry point for multiple Azure services.

Here's how it works:

1. **Create a Private Link Service:** You create a Private Link Service for each type of Azure service you want to connect to privately.

2. **Link Multiple Services:** Once the Private Link Service is set up, you can link multiple Azure services to it. This means that a single Private Link Service can act as the access point for multiple Azure services of the same type.

3. **Connect to the Private Link Service:** In your virtual network, you create a private endpoint for the Private Link Service. This private endpoint allows you to connect to all the linked services through a single entry point.

**Example Use Case:**

Consider you have multiple Azure services like Azure SQL Database, Azure Storage, and Azure Key Vault. Instead of creating separate endpoints for each service, you create a Private Link Service for each service type. Then, you link Azure SQL Database, Azure Storage, and Azure Key Vault to their respective Private Link Services.

Now, within your virtual network, you create a private endpoint for each Private Link Service. This provides a consolidated and simplified way to securely connect to multiple Azure services without the need for individual endpoints for each service.

In summary, Azure Private Link Service is a solution to simplify the management of multiple private connections to various Azure services within your virtual network. It offers a more streamlined and centralized approach, making it easier to configure, monitor, and maintain private connectivity to multiple services.


Certainly, let's dive deeper into specific use cases for each networking solution to clarify their distinct purposes:

**Azure Service Endpoint:**

Use Azure Service Endpoint when:

1. **You want to optimize traffic flow for specific Azure services:** Azure Service Endpoint is ideal when you want to enhance the performance and security of the connection to specific Azure services such as Azure SQL Database, Azure Storage, or Azure Cosmos DB. By enabling a service endpoint for a subnet, the traffic from your virtual network to the specific service takes a direct and optimized route over the Azure backbone.

2. **You don't need to bring the service into your virtual network:** If you do not require the Azure service itself to be part of your virtual network, and you are primarily focused on improving connectivity to the service, Azure Service Endpoint is a suitable choice. This is often the case when the Azure service does not need to be accessed using private IP addresses within your network.

**Azure Private Endpoint:**

Use Azure Private Endpoint when:

1. **You need a more isolated and private connection to Azure services:** Azure Private Endpoint is designed for scenarios where you require a higher level of isolation and want to bring the Azure service directly into your virtual network. It provides a private IP address within your network to connect to the Azure service, ensuring a more secure and private communication channel.

2. **You want to access Azure services using private IP addresses:** If your security policies mandate that connections to Azure services should be made using private IP addresses within your virtual network, Azure Private Endpoint is the solution. It allows you to connect to services like Azure SQL Database, Azure Storage, and Azure Key Vault using private IPs, reducing exposure to the public internet.

In summary, Azure Service Endpoint is suitable when you want to optimize the traffic flow to specific Azure services without bringing the service itself into your virtual network. Azure Private Endpoint, on the other hand, is the choice when you need a more private and isolated connection, and you want to access Azure services using private IP addresses within your virtual network. The decision between the two depends on your specific security and connectivity requirements for each Azure service.

When you configure a Service Endpoint on an Azure service, such as Azure SQL Database or Azure Storage, the need for additional firewall and access control settings depends on your specific requirements and the security configuration of the Azure service.

1. **Service Endpoint with Public Access:**
   - If the Azure service was configured with public access before the Service Endpoint was added, the default public access rules apply. These rules might include allowing traffic from all public IP addresses. In this case, you typically don't need to configure additional firewall rules for your virtual network.

2. **Service Endpoint with Restricted Public Access:**
   - If, however, you have configured the Azure service to have restricted public access (e.g., by blocking all public IP addresses), you might need to rely on the Service Endpoint to allow traffic from your virtual network.

3. **Firewall and Access Control for Private Access:**
   - When you make the Azure service "private" by configuring a Service Endpoint, you may need to set up additional firewall rules and access controls to allow traffic from your specific virtual network or subnet. This is particularly relevant when you want to restrict access to the service only from your virtual network and prevent public internet access.

In summary, the need for additional firewall and access control settings depends on the initial public access configuration of the Azure service and whether you are transitioning to a more private access model using Service Endpoint. If the service had public access, firewall rules may have been configured for that scenario. When making the service private through a Service Endpoint, you might need to adjust firewall settings to align with your desired private network access requirements. Always refer to the specific documentation for the Azure service in question for detailed guidance on configuring access controls and firewalls.

Azure DNS
----------
DNS Hosting
Used to create safe and reliable DNS Zones.
Create records inside this Zones.

Naming Convention
Zone Name should be unique in different resource groups.
NOTE:- You can have same zone within multiple resource groups, in this case name servers will be different for these Zones.

Delegated Zones

RecordSets
Records having same name and type are grouped together to form recordsets.

Maximum number of records allowed to a recordset is 20 nd they need to be unique.

DNS Dataview tool for verifying the record sets.

Private DNS Zones 
----------------
Name resolution for services deployed within the Azure Virtual Network.

NSG
-----

Consists of Inbound and Outbound rules.
Filters traffic incoming and outgoing based on this rules from VNET.
Rulesets
Associated with Subnets or Network Interfaces
Multiple subnets and network interfaces can be associated with single NSG
Rules applied at subnet and network interfaces is evaluated separately

Is based on rules. Everything is evaluated based on priority.
Default rules cannot be modified or deleted.
They can be overridden by creating rules with higher priority.
Rules can be created based on following attributes besides ip details:
Service: Http, Https, Ssh, RDP

Port range:

Priority: Lower number higher priority. Range from 100-4096. Values in 65000 range is for default rules.

Action: Allow or Deny

Azure Firewall
--------------
Highly Available and Scalable
Redundancy
Multiple types of rules
Threat Intelligence
Public IP Support

NSG is basic firewall and operates at the network layer 4. Filters traffic at individual resources.
Azure Firewall is managed and operates at the application layer 7. Filters traffic at the VNET level.

Azure Firewalls ar Global and can support multiple subnets.

Azure Firewall blocks traffic by default. 

3 types of Azure Firewall rules are:
----------------------------------------
NAT Rules - Routing Rule that allows traffic from public ip address to private ip address.
Network Rules
Application Rules

https://petri.com/the-three-different-types-of-rules-that-are-in-the-azure-firewall/


Virtual Machines Planning
-------------------------

Networking - Address Space to be planned based on Number of Hosts planned to be created. Size of the Hosts. IP Address Space should not overlap. Need for Subnet or Public IPs.

Naming Convention - Environment, role, service, region to VM names.

Location - Check availability of VM Sizes in different Azure Regions. Choos Low Cost regions if ok with data residency. Azure has 60+ regions.

Pricing - Reserved instances or pay-as-you-go pricing model for contract done for 1 to 3 yrs period. Spot VM for low priority development. Licensing cost can be reduced by Azure Hybrid Benefits.

Reserved instances are commitments to specific VM Sizes in specific regions for 1 or 3 year period providing discount as compared to pay-as-you-go pricing model.
https://learn.microsoft.com/en-us/answers/questions/108078/reserved-instances-vs-spot

Virtual Machine Sizing
----------------------

General Purpose - Development and Testing, small to medium DBs, low to medium traffic webservers

Compute Optimized - High CPU to memory ratio - Web Servers, Network Appliances, Batch Processes, Application Server

Memory Optimized - High Memory to CPU ratio - Relational DB, Caches, In-memory analytics

Storage Optimized - High Disk throughput and io - Big Data No SQL, Transaction DB, Data Warehouse

GPU - Graphics rendering, Video Editing and AI Deep Learning

HPC - Fastest and most Powerful VMs

Confidential Computing - Banks and Hospitals for PII data


Virtual Machine Storage
-----------------------
OS Disk - OS
Temporary Disk - Temp Data like page files. Data lost on resizing the VM. Ramins on the host.
Data Disk - Application Data
OS Disk and Data Disk are stored on Azure Blob Storage.

NOTE: -If the Size of the VM is small, the number of Data Disks that could be accomodated will also be less.

Performance Tiers - Standard HDD, Standard SSD, Premium SSD, Ultra SSD for IOPS and Performance

Management - Managed Disk and UnManaged disk. UnManaged Disk, customer to own the management or storage of VHD file on Azure Storage. Managed Disk is managed by Microsoft and is recommened by Microsoft.

Connecting to VMs
-----------------

Public IP

JumpBox

Azure Bastion


High Availability
-----------------

3 reasons for downtime:

Unplanned Hardware Maintenance - When there is a problem with physical server hosting VM, Azure Predicts it and does Live Migration of VM from one physical server to other which is healthy. VM will be paused for sometime leading to performance issues.

Unexpected downtime - Failure of networking, storage or rack issues. Azure will heal the VM by re-deploying the VM to health Server in same DataCenter. This will cause re-boot operation resulting in loss of data in temp drive.

Planned Maintenance - Updates and maintenance for security, reliability and performance of hardware on which VMs are running. Most of the time done without any downtime.



Geography is an area where we have multiple regions.

Each region has multiple DataCentres.

Availability Zones
------------------
DataCentre grouped together are called Availability Zones. Each AZ has power, cooling and networking component.

Availability Set
----------------

Multiple VMs to have control where the VM is deployed. Gives 99.95% SLA. Single VM is a single point of failure. If power goes down, then it leads to unavailability. Availability Set is at DataCenter level. If DataCenter goes down then VM goes down, hence Availability Zone.
2 Concepts of Availability Set

- Update Domain - During Planned Maintenance physical servers may need a reboot and that would take your VM offline. By deploying the VMs in multiple Fault Domains, Microsoft ensures that only one Domain is updated at a time. With Update Domain, Azure can ensure sequential update are done on physical servers ensuring availability. There are 5 Update Domains. Can update upto 20. Combination of Update and Fault Domain is called Availability Set.

- Fault Domain represent physical servers/racks within a DataCenter that share common networking, power and cooling.Deploying VMs across this Fault Domains, we could prevent the VM from hardware failure.


Azure Load Balancer
--------------------
Layer 4 LB over TCP/UDP.
Supports only VM and VMSS as the backend pool.
Load Balancing Rules
Inbound NAT Rules to specific machine on specific port for targeted access.
Outbound Rules

Sesssion Persistence
--------------------
None  - also called 5 tuple hash using Source IP, Destination IP, Source Port, Destination Port, Protocol to distribute traffic to the server. Useful for Stateless Application where session affinity is not required.
Client IP - also called 2 tuple hash based on Source IP and Destination IP. Useful for scenarios where we need to maintain the user session within the same session such E-commerce website. Sessions that need consistent server-side cache.
Client IP and Protocol- 3 tuple hash based on Source IP, Destination IP and Protocol. Useful for scenarios where different services on the same VM need to maintain sessions such as secure and non-secure connections to diff servers and services.


Azure Application Gateway
-------------------------
Layer 7 LB over HTTP/HTTPS/HTTP2/WebSocket.
Web Application Firewall can be added as optional component to the App Gateway.
Routing done based on url also called path based request routing. Can host multiple websites behind the App Gateway.
Url Rewrite, SSL Termination, Rewriting http headers, Custom Error Pages supported.
Supports VM, VMSS, Azure App Services, Deployment Slots and other servers deployed in other cloud providers and on-premise servers.
Path-based and Multi-Site routing.

Other Load Balancing Solutions
------------------------------
Azure Front Door
----------------
Provides fast content delivery.
Global solution and makes use of Microsoft Edge network.
Path-based and Multi-Site routing available and also WAF available as optional component.

Azure Traffic Manager
---------------------
DNS-based Load Balancer.
Finds best endpoint based on routing.
Routing logic includes Priority, Weighted, Geography.
Have nested profiles in Azure Traffic Manager.
Does not care about protocol because its a DNS based load balancing solution.

Network Watcher
---------------
Suite of tools to designed to monitor, diagnose and gain insight into network performance and network health in the Azure environment.

IP Flow Verify - Verify whether packets allowed to move to and from the VM

Next Hop - Verify whether the packet reaches the target in the VNET

VPN Diagnostics - Verify whether the connectivity from on-premise to Azure works

NSG Flow Logs - Verify Egress and Ingress traffic through NSG

Connection Troubleshoot - Verify any connectivity issues

Topology - Visual representation of Azure Resources within a VNET. Helps in understanding the architecture.

Azure Storage Accounts
----------------------
Standard and Premium

Azure Storage Redundancy
------------------------
LRS - 3 Copies on fault domain in single DC single region. Prevents hardware failure but not the DC failure.
ZRS - 3 Copies on 3 Zones(DC) in single region. Prevents the DC failure but not Region failure.
GRS - 3 Copies on fault domain in single DC primary region. Geo-Replication aysnc on 3 Copies on fault domain in secondary region. LRS + LRS. Secondary region is ReadOnly and will be available when there is a failover on primary region being unavailable. Prevents Region failure. Failover can be customer or Microsoft initiated. If new data needs to be written to Primary Region when is down, then application mechanism using Queues should be implemented.
RA-GRS - Same as LRS + LRS. But data can be read from Secondary Region without failover and also on failover it works like GRS.
GZRS - ZRS + LRS. 3 copies in Zones of Primary Region. 3 Copies in fault domain of Secondary Region.















