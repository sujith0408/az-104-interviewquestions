# az-104-interviewquestions

Azure AD

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





