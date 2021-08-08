# Storage Accounts  

## Intro  

Storage type:  
- General-purpose v1 / v2  
- BlobStorage  
- BlockBlobStorage  
- FileStorage  

Features:  
- Supported Services (What can I put in this storage account?):  
  - Blob  
  - File  
  - Queue  
  - Table  
  - Disk  
  - Data Lake Gen2  
- Performance Tiers (how fast will my read/writes be?)  
- Access Tiers (how often do I need quick access to files?)  
- Replication (how many redundant copies should be made and where?)  
- Deployment model (who sould deploy the supported services?)  

## Core Storage Services  

4 core storage services:  

- Azure Blob: scalable object store for text and binary data  
- Azure Files: managed file shares  
- Azure Queues: NoSQL store  
- Azure Tables: messaging store  
- *Azure Disks*: volumes for Azure VMs  

## Performance Tiers  

- Premium  
  - SSD  
  - optimize for low-latency  
  - higher throughput  
  - use cases:  
    - interactive worloads  
    - analytics  
    - AI / ML  
    - data transformation  
- Standard  
  - HDD  
  - based on access tier  
  - use cases:  
    - backup / DRS  
    - media content  
    - bulk data processing  

## Access Tiers  

3 types for Standard storage:  
- Cool:  
  - infrequently accessed and stored for at least 30 days  
  - lower storage cost, higher access cost  
  - use cases:
    - short-term backup / DRS  
    - older media content not viewed frequently anymore but is expected 
to be available immediately  
- Hot:
  - data is accessed frequently  
  - highest storage cost, lowest access cost  
  - use cases:  
    - in active use or expected to be accessed frequently  
    - for processing and eventual migration to the cool access tier  
- Archive:  
  - rarely accessed and stored for at least 180 days  
  - lowest storage cost, highest access cost  
  - use cases:  
    - long-term backup, secondary backup and archival datasets  

## Replication and Data Redundancy  

Replication type:  
- Primary Region Redundancy (for disaster recovery and failovers):  
  - Locally Redundant Storage (LRS)  
  - Zone Redundant Storage (ZRS)  
- Secondary Region Redundancy (for disaster recovery and failovers):  
  - Geo Redundant Storage (GRS)  
  - Geo Zone Redundant Storage (GZRS)  
- Secondary Region Redundancy with Read Access (Read Replicas):  
  - Read Access Geo Redundant Storage (RA-GRS)  
  - Read Access Geo Zone Redundant Storage (RA-GZRS)  

### LRS & ZRS  

Data is replicated 3 times in the primary region  

2 options:  
- LRS:  
  - copies data synchronously in primary region  
  - 99.99999999999% durability  
  - cheapest option  
- ZRS:  
  - copies data synchronously across 3 AZ in primary region  
  - 99.999999999999% durability  

### GRS & GZRS  

- Replicate to a secondary region in case of primary regional disaster  
- Secondary region is dertermined base on your primary's pair region  
- Secondary region isn't available for read/write access (except for failover)  

2 options:  
- GRS:  
  - copies data synchronously in primary region  
  - copies data asynchronously to another region  
  - 99.9999999999999999% durability  
- ZRS:  
  - copies data synchronously across 3 AZ in a physical region  
  - copies data asynchronously to another region  
  - 99.9999999999999999% durability  

### RA-GRS & RA-GZRS  

- Data is replicated synchronously to primary region  
- data will be "in-sync"  

## Azure Blob  

### Intro  

Object-store optimized for storing massive amounts of unstructured data  

Storage account: unique namespace in Azure for your data  
Containers: similar to a folder in a file system  
Blobs: data being stored  

### Blob types  

1. Block blobs  

- store text and binary data  
- can be managed individually  
- store up to about 4.75 TiB of data  

2. Append blobs  

- optimized for append operations  
- ideal for scenarios such as logging data from VM  

3. Page blobs  

- store random access files up to 8TB in size  
- storage virtual hard drive (VHD) files and serve as disks for Azure VM  

### Moving data  

Multiple wyas to move data into Azure Blob Storage:  

- `AzCopy`: cli tool  
- Azure Storage Data Movement library: .NET library (uses AzCopy underneath)  
- Azure Data Factory  
- Blobfuse  
- Azure Data Box  
- Azure Import / Export service  

## Azure Files  

File share in the cloud  

### Use cases  

- replace or supplement on-premises file servers NAS devices  
- lift-and-shift on premise to Cloud  
- simplify cloud development  
- Containerization  

### Features  

- Backups with shared snapshots  
  - read-only  
  - incremental  
  - up to 200 snapshots per file share  
  - retained up to 10 years  

- Soft Delete

- Advanced Threat Protection

- Store Tiers  
  - Premium  
  - Transaction optimized  (standard)  
  - Hot: team shares and Azure File Sync  
  - Cool: online archive  

- Type of storage  
  - GPv2: HDD  
  - FileStorage: SSD  

- Identity  
  - on-premise  
  - managed  
  - Store Account Key  

- Networking  
  - accessible via storage account public endpoint  
  - SMB connects to port 445  

- Encryption  
  - encrypted-at-rest  
  - encrypted-in-transit  

## Azure File Sync  

Cache Azure file shares (= like OneDrive) 

## Azure Storage Explorer  

Standalone app for working with Azure Storage Data  

## AZCopy  

CLI to copy blobs or files  

Check the level of authorization:
- to download:  
  - Storage Blob Data Reader  
- to upload:  
  - Storage Blob Data Contributor  
  - Storage Blob Data Owner  

Gain access via:  
- Azure Active Directory  
- Shared Access Signature  

## Azure Import/Export service  

Import large amounts of data to Azure Blob storage  

## Shared Access Signatures  

An URI that grants restricted access rights to Azure Storage resources  

Types:  
- Account-level SAS  
- Service-level SAS  
- User delegation SAS  

Different formats:  
- Ad hoc SAS  
  - start, expiry times and permissions are part of the URI  
  - any type of SAS can be an ad hoc SAS  
- Service SAS with stored access policy  
  - defined on a resource container  

Example of SAS URI:  

```
https://myaccount.blob.core.windows.net/?restype=service&amp;comp=properties&amp;sv=2015-04-05&amp;ss=bf&amp;srt=s&amp;st=2015-04-29T22%3A18%3A26Z&amp;se=2015-04-30T02%3A23%3A26Z&amp;sr=b&amp;sp=rw&amp;sip=168.1.5.60-168.1.5.70&amp;spr=https &amp;sig=F%6GRVAZ5Cdj2Pw4txxxxx
```

## Follow along  

### Use AZCopy to copy files to Storage Accounts    

- Create a Storage Account  

```
Storage Accounts
└ Create
  ├ Resource group
  ├ Storage account name
  ├ Region
  ├ Performance
  | ├ Standard
  | └ Premium
  ├ Redundancy
  └ Create
```

- Give Storage Account permission  

```
Storage Accounts
└ ## select Storage Account ##
  └ Access Control (IAM)
    └ Add role assignement
      ├ Select a role: Storage Account Contributor / Storage Account Owner
      ├ Assign access to: User, group. or service principal
      └ Select: Brian
```

- Use `azcopy`  

  - Login

```
$ azcopy login --tenant-id <tenant_id>
```

Use Brian's credentials  

  - copy a file to the container `fajotest` into the blob `fajotestsa`
```
$ azcopy cp helloworld.txt https://fajotestsa.blob.core.windows.net/fajotest/helloworld.txt
```

- Use Shared Access Signature    

  - Generate SAS token and URL  

```
Storage Accounts
└ ## select Storage Account ##
  └ Shared access tokens
    ├ [X] Signing method: Account key
    ├ Signing key: Key 1
    ├ Permission: 7 selected
    ├ Start and expiry date/time
    └ Generate SAS token and URL
```

  - Copy the URL and use `azcopy`  

```
azcopy cp helloworld.txt "https://fajotestsa.blob.core.windows.net/fajotest?sp=racwdli&st=2021-08-08T14:54:08Z&se=2021-08-08T22:54:08Z&spr=https&sv=2020-08-04&sr=c&sig=hXOEj5pabVeX8RqQ%2FzCfkxhH6wnOhIhdU88GsEblOZo%3D"
```

### Create a File Share with Azure Files    

- create Azure File share  

```
Storage Accounts
└ File Shares
  └ New File Share
    ├ Name: testsharefile
    ├ Tier: Key 1
    └ Create
```

- connect the File share to a Linux VM  

```
Storage Accounts
└ ## select Storage Account ##
  └ File Shares
    └ ## select File share ##
      └ Connect: Linux
```

  - follow the instructions to create the mount point to the Linux VM  

### Setup Azure Files Sync  

```
Home
└ Create a resource
  └ search: Azure File Sync
    ├ Resource group: testrg
    ├ Name: testfilesync
    ├ Region: France Central
    └ Create
```

> **_TODO_**: Do and document this follow along    

## Exercises  

> **_TODO_**: Do and document these exercises  

- Knowledge check - [Configure storage accounts](https://docs.microsoft.com/en-us/learn/modules/configure-storage-accounts/8-knowledge-check)  

- Knowledge check - [Configure blob storage](https://docs.microsoft.com/en-us/learn/modules/configure-blob-storage/9-knowledge-check)  

- Exercise - [Create a storage account using the Azure portal](https://docs.microsoft.com/en-us/learn/modules/create-azure-storage-account/5-exercise-create-a-storage-account)  

- Knowledge check - [Create a storage account](https://docs.microsoft.com/en-us/learn/modules/create-azure-storage-account/6-knowledge-check)  

- Exercise - [Use shared access signatures to delegate access to Azure Storage](https://docs.microsoft.com/en-us/learn/modules/control-access-to-azure-storage-with-sas/4-exercise-use-shared-access-signatures)  

- Exercise - [Use stored access policies to delegate access to Azure Storage](https://docs.microsoft.com/en-us/learn/modules/control-access-to-azure-storage-with-sas/6-exercise-use-stored-access-policies)  

- Exercise - [Create and connect to an Azure Files share](https://docs.microsoft.com/en-us/learn/modules/store-and-share-with-azure-files/4-exercise-create-azure-files)  

- Exercise - [Secure access to files stored in Azure Files](https://docs.microsoft.com/en-us/learn/modules/store-and-share-with-azure-files/6-exercise-secure-azure-files)  

- Exercise - [Connect Azure Storage Explorer to a storage account](https://docs.microsoft.com/en-us/learn/modules/upload-download-and-manage-data-with-azure-storage-explorer/3-exercise-connect-storage-account)  

- Exercise - [Connect Azure Storage Explorer to Azure Cosmos DB and Data Lake](https://docs.microsoft.com/en-us/learn/modules/upload-download-and-manage-data-with-azure-storage-explorer/5-exercise-connect-cosmosdb-data-lake)  
