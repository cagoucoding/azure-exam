# Azure AD

## Intro  

4 editions:  

- **Free** MFA, SSO, Basic Security and Usage Reports, User Management  
- **Office365 Apps** Company Branding, SLA, 2-sync between on-prem and cloud  
- **Premium 1 (P1)** Hybrid architecture, Advanced Group Access, Conditional Access  
- **Premium 2 (P2)** Identity Protection, Identity Gouvernance  

## Use case  

Authorize and authenticate to multiple sources:

- on-premise AD -> Azure AD Connect  
- web app -> App Registrations  
- allow users to login with their ipD (Facebook or Google) -> External Identities  
- to Office365 or Azure Microsoft  

## AD terminology  

- **Domain**: logical grouping  
- **Domain Controller (DC)**: server that authenticates and authorizes  
- **Domain Computer**: computer that is registred with a central authentication database  
- **AD Object**: basic element of AD  
- **Group Policy Object (GPO)**: virtual collection of policy settings
that controls what AD Objects have access to  
- **Organization Units (OU)**: subdivision within an AD into which you can place
users, groups, computers and OU  
- **Directory Service**: provides the methods for storing directory data and
making this data available to network users and administrators  

## Tenant

Represents an organization in Azure AD.  
Each Azure AD tenant is distinct and separate from other Azure AD tenants  

## Azure Active Directory DOmain Services (AD DS)  

In some case, need to setup own DC: *when doing a lift-and-shift on-premise 
to Microsoft Azure and migratin AD, Azure AD doesn't support some domain services*  

AD DS provides managed domaine service:  
- Domain joins  
- Group policies  
- LDAP  
- Kerberos  

## Azure AD Connect  

Single Sign On from your on-premise workstation to MS Azure  

## Users  

Identity for a person or an employee  

2 kinds of users:  
- Users  
- Guest Users  

## Groups  

Contain:  
- Owners: permissions to add and remove members  
- Members: permissions to do things  

You can assign:  
- roles directly to a group  
- applications directly to a group  

Members can request to join a group  

## Assign Access Rights

4 ways:  
- direct assignment: resource owner directly assigns the user to the resource  
- group assignment: resource owner assigns an Azure AD group to the resource 
which automatically gives all of the group members access to the resource  
- Rule-based assignment: resource owner creates a group and uses a rule to define 
which users are assigned to a specific resource  
- External authority assignment: access comes from an external source  

## External Identities  

Can bring their own identities

## Follow along  

### Create a Tenant  

```
Azure Active Directory
??? Manage tenants
  ??? Create
    ??? Tenant type: Azure Active Directory
    ??? Org name: Cagou Coding
    ??? Initial domain name: cagoucoding
    ??? Country: France
```

### Upgrade License

```
Azure Active Directory
??? Licenses
  ??? All products
    ??? Tenant type: Azure Active Directory
    ??? Org name: Cagou Coding
    ??? Initial domain name: cagoucoding
    ??? Try / Buy
      ??? Activate: Azure AD Premium P2   
```

### Users and Groups  

#### Create a Group  

```
Azure Active Directory
??? Groups
  ??? New group
    ??? Group type: Security
    ??? Group name: developers
    ??? Group description: Developers of Cagou Coding
```

#### Create an User  

```
Azure Active Directory
??? Users
  ??? New user
    ??? [X] Create user 
    ??? User name: brian@cagoucoding.onmicrosoft.com
    ??? Name: Brian Cagoucoding
    ??? First name: Brian
    ??? Last name: Cagoucoding
    ??? [X] Auto-generate password -> Cohu8965
    ??? Groups: select the group -> developers
    ??? Roles: select the role -> Application developer
    ??? Additionnal info: ...
```

Deleted users are still available for 30 days  

### Guest Users  

Same as [a creation of an User](#create-an-user) but just to provide the email 
of the guest  

```
Azure Active Directory
??? Users
  ??? Invite user
    ??? [X] Create user 
    ??? Email: brian@cagoucoding.onmicrosoft.com
    ??? Name: Brian Cagoucoding
    ??? First name: Brian
    ??? Last name: Cagoucoding
    ??? Groups: select the group -> developers
    ??? Roles: select the role -> Application developer
    ??? Additionnal info: ...
```

### Mass import  

```
Azure Active Directory
??? Users
  ??? Bulk operations
    ??? Bulk create 
      ??? Download csv template
      ??? Edit csv file
      ??? Upload modified csv file
```

### Multi-Factor Authentication  

```
Azure Active Directory
??? Users
  ??? Per-user MFA
    ??? users 
    | ??? [X] Selected user
    |   ??? Enable
    ??? service settings 
      ??? [X] Allow users to create app passwords to sign in to non-browser apps
      ??? Verification options -> Methods available: SMS / Notif through mobile app / Token
```

### Self-service reset password  

```
Azure Active Directory
??? Password reset
```

**NB**: It needs Premium license  

## Exercises  

> **_TODO_**: Do and document these exercises  

- Exercise - [Add and delete users in Azure Active Directory](https://docs.microsoft.com/en-us/learn/modules/create-users-and-groups-in-azure-active-directory/3-exercise-add-delete-users-azure-ad)  
- Exercise - [Assign users to Azure Active Directory groups](https://docs.microsoft.com/en-us/learn/modules/create-users-and-groups-in-azure-active-directory/5-exercise-assign-users-azure-ad-groups)  
- Exercise - [Give guest users access in Azure Active Directory B2B](https://docs.microsoft.com/en-us/learn/modules/create-users-and-groups-in-azure-active-directory/7-exercise-guest-user-access-azure-ad-b2b)  
- Exercise - [Set up self-service password reset](https://docs.microsoft.com/en-us/learn/modules/allow-users-reset-their-password/4-exercise-set-up-self-service-password-reset)  


# AD Device Management  

## Intro  

Management of physical devices - phones, tablets, laptops and desktop computers - 
granted access to company resources via **device-based Conditional Access**  

Under Azure portal section:  
```
Azure Active Directory
??? Devices
```

3 ways to get devices into Azure AD:

- Azure AD Registred  
  - personally owned or mobile devices  
  - signed in with personal Microsoft or local account  

- Azure AD Joined  
  - owned by organization  
  - signed in with an Azure AD account belonging to the organization  
  - only exist in the cloud  

- Hybrid Azure AD Joined  
  - owned by organization  
  - signed in with an AD domain Services account belonging to the orga  
  - exist in the cloud and on-prem  

## AD Registered Devices  

## Windows Hello  

Alternative way to log into their devices and app:  

- fingerprint  
- iris scan  
- facial recognition  

## Mobile Device Management (MDM) & Mobile Application Management (MAM)  

- MDM  
  - control the entire device  
  - wipe data  
  - reset to factory settings  

- MAM  
  - publish / push / configure / secure / monitor / update mobile apps  

Managed via **Microsoft Intune** -> needs Azure AD Premium 2  

**NB**: Intune = Endpoint Manager = EMS  

## Microsoft Enterprise Mobility + Security (EMS)  

An umbrella of multiple Microsoft and Azure services -> Azure AD & Microsoft Itune  

## Microsoft Authenticator  

App for secure sign-ins  

## AD Joined Devices  

## FIDO2 Security Keys  

Fast Identity Online Alliance: industry association which develop and promote 
authentication standards to help reducing the world's over-reliance on passwords  

3 sets of open specifications:  
- FIDO Universal Second Factor (FIDO U2F)  
- FIDO Universal Authentication Framework (FIDO UAF)  
- Client to Authenticator Protocols (CTAP)  
- CTAP is complementary to the W3C's Web Authentication (WebAuthn) -> FIDO2  

**Security key**: secondary device used as a second step in authentication 
process to gain access to a device, workstation or application  (ex: Yubikey)  

## Hybrid Azure AD Joined Devices  

## Windows Autopilot  

Collection of technologies used to set up and pre-configure new devices 
for being production-ready  

# Roles  

## Types of Roles  

3 types of Roles which can serve same purpose:  

- Classic subscription administrator roles: original role system  
- Azure roles: RBAC system built on top of Azure Resource Manager  
- Azure AD roles: used to managed Azure AD resources in a directory  

## IAM Access Controls  

Identity Access Management (IAM) allows you to create and assign roles to users  

### Azure Roles (RBAC system)  

Roles restrict access to resource actions (operations)  

- BuiltInRole: Managed Microsoft roles are read-only pre-created roles  
- CustomRole: created by you with your own custom logic  

### Role assignments  

Apply a role to:  
- Service Principal  
- User / Group  

### Deny assignments  

Block users from performing specific actions -> through Azure BluePrints  

### Classic Administrators  

**WARNING**: Original role system but should use the new RBAC System  

- Account Administrator: billing owner of the subscription but no access to Azure portal  
- Service Administrator = Owner role at subscription scope  
- Co-Administrator = Owner role at subscription scope  

## RBAC  

Helps you manage who has access to Azure resources  

Roles assignments:  

- security principal represents the identities requesting access to an Azure 
resource:  
  - *User*: an individual who has a profile in Azure AD  
  - *Group*: a set of users  
  - *Service Principal*: used by applications or services  
  - *Managed Identity*: identity in Azure AD that is automatically managed by Azure  

- role definition is a collection of permissions: read / write / delete  

- scope is the set of resources for the Role Assignment applies to  

There are 4 fundamental Azure roles:  
- Owner  
- Contributor  
- Reader  
- User Access Administrator  

RBAC includes 70 built-in roles  

## Azure AD roles  

To manage Azure AD resources:  

- create or edit users  
- assign administrative roles to others  
- reset user passwords  
- manage user licenses  
- manage domains  

Important AD roles:  
- Global Adminstrator  
- User Administrator  
- Billing Administrator  

## Azure Roles  

## Azure Policies vs. Azure Roles (RBAC)  

Azure policies | Azure Roles
--- | ---
Ensure compliance of resource | Control access to Azure resources  

## Azure AD roles vs. Azure Roles (RBAC)  

| Azure AD Roles | Azure Roles |
| --- | --- |
| Control access of AD resources | Control access to Azure resources |
| <ul><li>Users</li><li>Groups</li><li>...</li></ul> | <ul><li>Virtual Machines</li><li>Databases</li><li>...</li></ul> |  

## Exercises  

> **_TODO_**: Do and document these exercises  

- Exercise - [Get access to an Azure subscription](https://docs.microsoft.com/en-us/learn/modules/manage-subscription-access-azure-rbac/4-exercise-elevate-permissions)  
- Knowledge check - [What is Azure RBAC?](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/3-knowledge-check-rbac-overview)  
- Exercise - [List access using Azure RBAC and the Azure portal](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/4-list-access)  
- Exercise - [Grant access using Azure RBAC and the Azure portal](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/5-grant-access)  
- Exercise - [View activity logs for Azure RBAC changes](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/6-view-activity-logs)  
- Knowledge check - [Using Azure RBAC](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/7-knowledge-check-rbac)  
- Exercise - [Create an Azure custom role](https://docs.microsoft.com/en-us/learn/modules/create-custom-azure-roles-with-rbac/3-exercise-create-custom-role)  
- Exercise - [View and manage an Azure custom role](https://docs.microsoft.com/en-us/learn/modules/create-custom-azure-roles-with-rbac/5-exercise-manage-custom-roles)  


# Azure Policies  

## Intro  

Enforce organizational standards and to assess compliance at-scale  

- Policy Definitions: JSON file to describe business rules to control access 
to resources  
- Policy Assignment: Scope of a policy can effect (User, Resource Group or Management Group)  
- Policy Parameters: Values passed into Policy definition  
- Initiative Definitions: Collection of policy definitions  

## Non-compliant Resources  

```
Policy
??? Compliance
  ??? Non-compliant policies (list)
```

## Azure Policy Definition  

## Technical Pratice  

### Configure Policy  

> **_TODO_**: Do and document these exercises  

- Assign Policy `Audit virtual machines without disaster recovery configured` 
to a virtual machine  

#### Exercises  

> **_TODO_**: Do and document these exercises  

- Exercise - [Restrict deployments to a specific location by using Azure Policy](https://docs.microsoft.com/en-us/learn/modules/build-cloud-governance-strategy-azure/9-restrict-location-azure-policy)  
- Knowledge check - [Build a cloud governance strategy on Azure](https://docs.microsoft.com/en-us/learn/modules/build-cloud-governance-strategy-azure/11-knowledge-check)


# Azure Resource Manager  

## Intro  

To manage Azure resources:
- Create  
- Update  
- Delete    

## Use cases  

ARM is a gate keeper: all requests flow through ARM and it decides whether 
that request can be performed on a resource  

## Scoping  

Boundary of control for Azure resources:  

Management Groups -> Subscriptions -> Resource Groups -> Resources  

### Management Groups  

To manage multiple subscriptions  

### Subscriptions  

Can have multiple Subcriptions:  
- Free Trial  
- Pay-As-You-Go  
- Azure for Students    

From Subscription level, many abilities:

```
Subscriptions
??? Resources Tags
??? Access control (IAM) 
| ??? Roles
| ??? Roles assignments
| ??? Deny assignments
| ??? Classic administrators
??? Resources Groups 
??? ...
```

### Resources Groups  

Contain related Azure resources  

### Resources Providers  

For using Azure resources, you have to register Resources Providers  

### Resources Tags  

< Key, Value > pair that you can assign to Azure resources  

To organize in differents ways:  
- Resource management  
- Cost management and optimization  
- Operations management  
- Security  
- Governance and regulatory compliance  
- Automation  
- Workload optimization  

### Resource Locks  

Need to lock a Subscription / RG / Resource to prevent other users from accidentally deleting or modifying critical resources  

2 modes:  
- CanNotDelete
- ReadOnly  

### Azure Blueprints  

Quick creation of **governed Subscriptions**  

Declarative way to orchestrate the deployment of various resource templates and other artifacts:  

- Role Assignments  
- Policy Assignments  
- ARM templates  
- Resource Groups  

=> *Azure Cosmos DB*  

## Follow along  

### Moving resources  

Two RG:  
- `rg1`  
- `rg2`  

`disk1` created in `rg1`  

- moving `disk1` from `rg1` to `rg2`  

```
Resources Groups
??? rg1
  ??? [X] disk1 
    ??? Move 
      ??? Move to another resource group
      ??? Move to another subscription
      ??? Move to another region
```

- create a Lock to `rg2` to forbid deletion and moving of resources  

```
Resources Groups
??? Locks
  ??? Add lock 
    ??? Lock name
    ??? Lock type
    | ??? Read-only
    | ??? Delete
    ??? Notes
```

- try to delete / move `disk1` out to `rg2`

## Exercises  

> **_TODO_**: Do and document these exercises  

- Exercise - [Identify incorrectly assigned resources](https://docs.microsoft.com/en-us/learn/modules/move-azure-resources-another-resource-group/3-exercise-identify-incorrectly-assigned-resources)  

- Exercise - [Move and verify resources between Azure resource groups](https://docs.microsoft.com/en-us/learn/modules/move-azure-resources-another-resource-group/7-exercise-move-verify-resources)  
