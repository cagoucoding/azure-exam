# FreeCodeCamp

## Azure AD

### Intro  

4 editions:  

- **Free** MFA, SSO, Basic Security and Usage Reports, User Management  
- **Office365 Apps** Company Branding, SLA, 2-sync between on-prem and cloud  
- **Premium 1 (P1)** Hybrid architecture, Advanced Group Access, Conditional Access  
- **Premium 2 (P2)** Identity Protection, Identity Gouvernance  

### Use case  

Authorize and authenticate to multiple sources:

- on-premise AD -> Azure AD Connect  
- web app -> App Registrations  
- allow users to login with their ipD (Facebook or Google) -> External Identities  
- to Office365 or Azure Microsoft  

### AD terminology  

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

### Tenant

Represents an organization in Azure AD.  
Each Azure AD tenant is distinct and separate from other Azure AD tenants  

### Azure Active Directory DOmain Services (AD DS)  

In some case, need to setup own DC: *when doing a lift-and-shift on-premise 
to Microsoft Azure and migratin AD, Azure AD doesn't support some domain services*  

AD DS provides managed domaine service:  
- Domain joins  
- Group policies  
- LDAP  
- Kerberos  

### Azure AD Connect  

Single Sign On from your on-premise workstation to MS Azure  

### Users  

Identity for a person or an employee  

2 kinds of users:  
- Users  
- Guest Users  

### Groups  

Contain:  
- Owners: permissions to add and remove members  
- Members: permissions to do things  

You can assign:  
- roles directly to a group  
- applications directly to a group  

Members can request to join a group  

### Assign Access Rights

4 ways:  
- direct assignment: resource owner directly assigns the user to the resource  
- group assignment: resource owner assigns an Azure AD group to the resource 
which automatically gives all of the group members access to the resource  
- Rule-based assignment: resource owner creates a group and uses a rule to define 
which users are assigned to a specific resource  
- External authority assignment: access comes from an external source  

### External Identities  

Can bring their own identities

### Create a Tenant  

```
Azure Active Directory
    └ Manage tenants
        └ Create
          ├ Tenant type: Azure Active Directory
          ├ Org name: Cagou Coding
          ├ Initial domain name: cagoucoding
          └ Country: France
```

### Upgrade License

```
Azure Active Directory
    └ Licenses
        └ All products
          ├ Tenant type: Azure Active Directory
          ├ Org name: Cagou Coding
          ├ Initial domain name: cagoucoding
          └ Try / Buy
              └ Activate: Azure AD Premium P2   
```

### Users and Groups  

#### Create a Group  

```
Azure Active Directory
    └ Groups
        └ New group
          ├ Group type: Security
          ├ Group name: developers
          └ Group description: Developers of Cagou Coding
```

#### Create an User  

```
Azure Active Directory
    └ Users
        └ New user
          ├ [X] Create user 
          ├ User name: brian@cagoucoding.onmicrosoft.com
          ├ Name: Brian Cagoucoding
          ├ First name: Brian
          ├ Last name: Cagoucoding
          ├ [X] Auto-generate password -> Cohu8965
          ├ Groups: select the group -> developers
          ├ Roles: select the role -> Application developer
          └ Additionnal info: ...
```

Deleted users are still available for 30 days  

### Guest Users  

Same as [a creation of an User](#create-an-user) but just to provide the email 
of the guest  

```
Azure Active Directory
    └ Users
        └ Invite user
          ├ [X] Create user 
          ├ Email: brian@cagoucoding.onmicrosoft.com
          ├ Name: Brian Cagoucoding
          ├ First name: Brian
          ├ Last name: Cagoucoding
          ├ Groups: select the group -> developers
          ├ Roles: select the role -> Application developer
          └ Additionnal info: ...
```

### Mass import  

```
Azure Active Directory
    └ Users
        └ Bulk operations
          ├ Bulk create 
            ├ Download csv template
            ├ Edit csv file
            └ Upload modified csv file
```

### Multi-Factor Authentication  

```
Azure Active Directory
    └ Users
        └ Per-user MFA
          ├ users 
            └ [X] Selected user
              └ Enable
          └ service settings 
            ├ [X] Allow users to create app passwords to sign in to non-browser apps
            └ Verification options -> Methods available: SMS / Notif through mobile app / Token
```

### Self-service reset password  

```
Azure Active Directory
    └ Password reset
```

**NB**: It needs Premium license  




# Udemy

## Manage Azure Subscriptions  

Creating / using a Subscription  

## Analyze Resource utilization and consumption  

### Azure Monitor and Alerts  

In [Monitor](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview) part.  

- Metrics  
  - select scope (resource type, ...)  
  - select metric (percentage CPU, disks IO, ...)

*Optional*: Pin to dashboard  

- Alerts  
  - select scope (resource) -> filter example: *Virtual machines*  
  - configure **condition** -> example: *Percentage CPU*  
    - operator -> Greater than Maximum 90 (*Whenever the maximum percentage cpu is greater than 90%*)  
    - evaluated based on -> period 5m and frequency every 1m  
  - add **action groups**  
    - Notifications -> Type *Email/SMS message/Push/Voice*, Name *Email*, edit with right values  
    - Actions -> ITSM, Automation Runbook, ITSM, Webhook  
  - create the rule  
    - select the action group  
    - fill name, description and severity rule  

### Log analytics  

First, create a [Log Analytics workspaces](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.OperationalInsights%2Fworkspaces)  

Into the created **Logs Analytics workspace**:  

- Connect VM  
  - **Workspace Data Sources**
    - **Virtual machines** -> click on the vm to connect to -> *Connect* button  
- Configure data sources  
  - **Agents configuration** (Windows event logs, Windows perf counters, Linux perf counters, Syslog, IIS logs)  
    - Add perf counter / facility  
- Get logs  
  - **Logs**  
    - Run query -> `Heartbeat | where TimeGenerated > ago(30m) | where Computer == "vm01"`  


