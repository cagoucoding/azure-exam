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

## Technical pratice

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

# AD Device Management  

## Intro  

Management of physical devices - phones, tablets, laptops and desktop computers - 
granted access to company resources via **device-based Conditional Access**  

Under Azure portal section:  
```
Azure Active Directory
    └ Devices
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
