# ARM Templates  

## Intro  

JSON files that define Azure resources:  
- declarative (get exactly what you define)  
- stand up, tear down or share entire architectures in minutes  
- reduce config mistakes  
- establish an architecture baseline for compliance  
- **Modularity**: break up your architecture in multiple files and reuse them  
- **Extensibility**: add PowerShell and Bash scripts to your templates  
- **Testing**: use the ARM template tool kit  
- **Preview Changes**: before infra creation, see what it will create  
- **Built-In validation**: only deploy ARM template if it passes  
- **Track Deployments**: keep track of changes to architecture over time  
- **Policy as Code**: apply Azure Policies to ensure remain compliant  
- **CI/CD integration**  
- **Exportable code**  
- **Authoring tools**: Vscode has advanced features for authoring ARM Templates  

## ARM Template Skeleton  

- `$schema` describes the structure of JSON data  
- `contentVersion` is the version of the template  
- `apiProfile` (optional) for avoiding to specify API versions for each resource in the template  
- `parameters` (optional) are values you can pass along to your template  
- `variables` (optional) transform parameters or resource properties using function expressions  
- `functions` (optional) are user-defined functions available within the template  
- `resources` are the wanted Azure resources to deploy or update  
- `output` (optional) is the values that are returned after deployment  

### Resources  

```json
{
   "$schema": "...",
   "contentVersion": "...",
   "apiProfile": "",
   "parameters": {},
   "variables": {},
   "functions": [],
   "resources": [
      {
          "type": "Microsoft.Storage/storageAccounts",
          "apiVersion": "2019-06-01",
          "name": "learntemplatestorage123",
          "location": "westus",
          "sku": {
              "name": "Standard_LRS"
          },
          "kind": "StorageV2",
          "properties": {
              "supportsHttpsTrafficOnly": true
          }
      }
   ],
   "outputs": {}
}
```

### Parameters  

```json
{
   "$schema": "...",
   "contentVersion": "...",
   "apiProfile": "",
   "parameters": {
     "storageName": {
       "type": "string",
       "defaultValue": "mystorage-fr",
       "minLength": 5,
       "maxLength":20
     }
   },
   "variables": {},
   "functions": [],
   "resources": [
      {
          "type": "Microsoft.Storage/storageAccounts",
          "apiVersion": "2019-06-01",
          "name": "[parameters('storageName')]",
          "location": "westus",
          "sku": {
              "name": "Standard_LRS"
          },
          "kind": "StorageV2",
          "properties": {
              "supportsHttpsTrafficOnly": true
          }
      }
   ],
   "outputs": {}
}
```

### Functions  

- Template functions: built-in functions  
  - Array  
  - Comparison  
  - Date  
  - Deployment  
  - Logical  
  - Numeric  
  - Object  
  - Resource  
  - String  
- User-Defined functions  

Functions are called using `()`  

```json
{
   "$schema": "...",
   "contentVersion": "...",
   "apiProfile": "",
   "parameters": {
     "storageName": {
       "type": "string",
       "defaultValue": "mystorage-fr",
       "minLength": 5,
       "maxLength":20
     }
   },
   "variables": {},
   "functions": [],
   "resources": [
      {
          "type": "Microsoft.Storage/storageAccounts",
          "apiVersion": "2019-06-01",
          "name": "[parameters('storageName')]",
          "location": "[if(contains(parameters('storageName'), '-fr'), 'centralfrance', 'westeurope')]",
          "sku": {
              "name": "Standard_LRS"
          },
          "kind": "StorageV2",
          "properties": {
              "supportsHttpsTrafficOnly": true
          }
      }
   ],
   "outputs": {}
}
```

### Variables  

```json
{
   "$schema": "...",
   "contentVersion": "...",
   "apiProfile": "",
   "parameters": {
     "storageName": {
       "type": "string",
       "defaultValue": "mystorage-fr",
       "minLength": 5,
       "maxLength":20
     }
   },
   "variables": {
     "defaultLocations": {
       "france": "centralfrance",
       "europe": "westeurope"
     }
   },
   "functions": [],
   "resources": [
      {
          "type": "Microsoft.Storage/storageAccounts",
          "apiVersion": "2019-06-01",
          "name": "[parameters('storageName')]",
          "location": "[if(contains(parameters('storageName'), '-fr'), [variables('defaultLocations')].france, [variables('defaultLocations')].europe)]",
          "sku": {
              "name": "Standard_LRS"
          },
          "kind": "StorageV2",
          "properties": {
              "supportsHttpsTrafficOnly": true
          }
      }
   ],
   "outputs": {}
}
```

### Output  

```json
{
   "$schema": "...",
   "contentVersion": "...",
   "apiProfile": "",
   "parameters": {
     "storageName": {
       "type": "string",
       "defaultValue": "mystorage-fr",
       "minLength": 5,
       "maxLength":20
     }
   },
   "variables": {
     "defaultLocations": {
       "france": "centralfrance",
       "europe": "westeurope"
     }
   },
   "functions": [],
   "resources": [
      {
          "type": "Microsoft.Storage/storageAccounts",
          "apiVersion": "2019-06-01",
          "name": "[parameters('storageName')]",
          "location": "[if(contains(parameters('storageName'), '-fr'), [variables('defaultLocations')].france, [variables('defaultLocations')].europe)]",
          "sku": {
              "name": "Standard_LRS"
          },
          "kind": "StorageV2",
          "properties": {
              "supportsHttpsTrafficOnly": true
          }
      }
   ],
   "outputs": {
     "resourceID": {
       "type": "string",
       "value": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageName'))]"
     }
   }
}
```

## Follow along  

### Launch an ARM template  

- In the portal, go to the following section

```
Deploy a custom template
└ Build your own template in the editor
  └ Add resource
    └ Select a resource to the template
      └ Ubuntu virtual machine
```

- modify the variables if needed  

![alt text](../images/arm_template_modify_variable.gif "Modifying ARM Template Variable")  

## Exercises  

> **_TODO_**: Do and document these exercises  

- Exercise - [Create and deploy an Azure Resource Manager template](https://docs.microsoft.com/en-us/learn/modules/create-azure-resource-manager-template-vs-code/3-exercise-create-and-deploy-template?pivots=cli)  

- Exercise - [Add parameters and outputs to your Azure Resource Manager template](https://docs.microsoft.com/en-us/learn/modules/create-azure-resource-manager-template-vs-code/5-exercise-parameters-output?pivots=cli)  

- Knowledge check - [ARM Templates](https://docs.microsoft.com/en-us/learn/modules/create-azure-resource-manager-template-vs-code/6-knowledge-check)  

# Virtual Machines  

## Intro  

- Size of the VM determined by the Image  
- 20 VMs per region  
- Billed at an hourly rate  
- 99.9% availability (with premium disks)  

## Sizes  

**Types**: General Purposes, Compute Optimized  
**Sizes** (also called Series or SKU family): B, Dsv3

## Azure Compute Units  

ACU provides a way of comparing compute (CPU) performance across Azure SKUs  

| SKU Family | ACU / vCPU | vCPU:Core |
| --- | --- | --- |
| A1 - A4 | 100 | 1:1 |
| D1 - D14 | 160 - 250 | 1:1 |

## VM Mobile App  

For monitoring and for doing basic operations in your VMs  

## Hyper-V  

Hardware virtualization product which allows you create and run software 
version of a computer  

2 generations:  
- Generation 1  
  - support most guest OS  
  - BIOS-based architecture  
- Generation 2  
  - support most 64-bits version of Windows and Linux OS  
  - UEFI-based boot achitecture  
  - secure boot  
  - larger boot volume up to 64 TB  

## Connection ways  

- SSH (port 22)  
- RDP (port 3389)  
- Bastions: with **Azure Bastion** service  

### SSH  

### RDP  

Download the RDP file and open it wit RDP app  

### Azure Bastion  

Intermediate harden instance you can use to connect to your target server via 
SSH or RDP  

Bastion should be in the same Vnet of the target VMs  

## Windows vs Linux servers  

- Windows  
  - need a Windows License (or Windows account unactivated)  
  - set username and password  
  - must use a much larger instances to run Windows at least a B2  
  - full desktop environments  
- Linux  
  - most version require no license  
  - small VM sizes  
  - terminal based environments  

## Update management  

It allows you to manage and install OS updates and patches:  
- need to install the Microsoft Monitoring Agent 
(**Azure Automations** is the underlying service)  
- perform a scan for update compliance performed every 12h on Windows and 
every 3h on Linux  
- 30 mins and 6h for dashboard to display updated data  

## Follow along  

### Create a Bastion  

After having created a VM `testbastion`

- Configure the VM as a Bastion 

```
Virtual machines
└ [X] Select virtual machine: testbastion
  └ Connect
    └ Use Bastion
      ├ Step 1: Add new CIDR 
      ├ Step 2: Create the Bastion subnet
      ├ Step 3: Create Bastion
      └ Create Azure Bastion using defaults
```

- Connect via user/password credentials to open a new window with RDP connection  

### Create Windows VM  

> **_TODO_**: Do and document these exercises  

### Create Linux VM  

> **_TODO_**: Do and document these exercises  

### VM monitoring  

> **_TODO_**: Do and document these exercises  

```
Virtual machines
└ [X] Select virtual machine: testbastion
  └ Diagnostic settings
    └ ...
      ├ ... 
      ├ ...
      └ ...
```

## Exercises  

> **_TODO_**: Do and document these exercises  

- Knowledge check - [Configure virtual machines](https://docs.microsoft.com/en-us/learn/modules/configure-virtual-machines/10-knowledge-check)  

- Exercise - [Create a Windows virtual machine](https://docs.microsoft.com/en-us/learn/modules/create-windows-virtual-machine-in-azure/3-exercise-create-a-vm)  

- Exercise - [Connect to a Windows virtual machine using RDP](https://docs.microsoft.com/en-us/learn/modules/create-windows-virtual-machine-in-azure/5-exercise-connect-to-a-windows-vm-using-rdp)  

# Azure Managed Disks  

## Intro  

- Block level storage volumes  
- 3 replicas of your data  
- create up to 50 000 VM disks of a type in a subscription per region  
- integrated with *availability sets* and support *availability zones*  
- **Azure Backup** for creating a backup job  

## Disk Encryption  

2 types:  

- Server Side Encryption (SSE)  
  - by default  
  - encryption-at-rest can be managed in 2 ways  
    - platform-managed keys  
    - customer-managed keys  

- Azure Disk Encryption (ADE)  
  - encryption the OS and Data disks  
  - BitLocker (Windows) / DM-Crypt (Linux)  

## Disk Roles  

- Data disk  
  - for storing application data  
  - max capacity of 32 767 GiB  
  - size of the VM determines how many data disks you can attach  

- OS disk  
  - contains pre-installed OS and boot volume  
  - max capacity of 4095 GiB  

- Temporary disk  
  - not managed disk  
  - short-term storage for applications and processes (page or swap files)  
  - data may be lost during a maintenance event  
  - data will persist during a successful standard reboot  
  - typically `/dev/sdb` or `D:`  

## Managed Disk Snapshots & Managed Custom Image  

**Managed disk snapshot** is a read-only crash-consistent full copy of a managed disk  

**Managed custom image** allows you to create an image of your disk from your VM (all disks)  

## Disk types  

4 tiers:  

- Ultra Disks  
  - suited for data-intensive worloads such as SAP HANA, top tier databases  
  - can only be used as data disks  
  - only supported with very specific VM series  

- Premium SSD  
  - suited for mission-critical production applications  
  - only be used with VM series that are premium storage-compatible  

- Standard SSD  
  - cost-effective storage option  
  - suited for web servers, low IOPS application servers, dev/test workloads  

- Standard HDD  
  - non critical  
  - infrequent access  

## Bursting  

Ability to boost disk storage IOPS and MB/s performance for a period of time 
on both VMs and disks  

## Follow along  

### Attach a data disk to a VM 

```
Virtual machines
└ [X] Select VM: testvm
  └ Disks
    └ Create and attach data disks
      ├ LUN: 0
      ├ Disk name: mysecondisk
      ├ Storage type: Standard SSD LRS
      └ Size (GiB): 4
```

### Backup a data disk  

```
Virtual machines
└ [X] Select VM: testvm
  └ Disks
    └ [X] Select disk: mysecondisk
      └ Create snapshot
        ├ Name: mysecondiskbackup
        ├ Storage type: Zone-redundant
        └ Create
```

# Application Gateway  