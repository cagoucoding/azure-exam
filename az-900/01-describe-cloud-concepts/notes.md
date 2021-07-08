# Introduction to Azure fundamentals

[source](https://docs.microsoft.com/en-us/learn/modules/intro-to-azure-fundamentals)

## Introduction

### Domain areas

AZ-900 Domain Area | Weight
--- | ---
Describe cloud concepts | 20-25%
Describe core Azure services | 15-20%
Describe core solutions and management tools on Azure | 10-15%
Describe general security and network security features | 10-15%
Describe identity, governance, privacy, and compliance features | 20-25%
Describe Azure cost management and Service Level Agreements | 10-15%

## What is cloud computing?

- Cheaper because *pay-as-you-go*  
  - lower operation costs  
  - run infra more efficiently  
  - more scalable  

## What is Azure?

- 100 services  
- [Azure portal](https://portal.azure.com/): Web based portal to manage all Azure services  
- [Azure markerplace](https://azuremarketplace.microsoft.com/): on-demand solutions and services  

## Tour of Azure services

- Compute: VM, Kubernetes, Functions  
- Networking: Virtual network, DNS, VPN, Loadbalancers
- Storage: BLOB, File storage  
- Mobile: Android / iOS backend  
- Database: Cosmos DB, SQL, MySQL, PostgreSQL  
- Web: web hosting  
- IoT: IoT software or edge  
- Big Data: Synapse Analytics, HDInsight, Databricks  
- AI  
- Devops  

## Azure accounts

![alt text](../images/get-started-azure-accounts.png "Azure scope levels")

- Learn sandbox: some exercises can create temporary subscription for the duration of the learn module

## Case study

**Tailwind Traders** manages on-premises datacenter for hosting company's retail website.  

IT department responsible for hardware and software management  

## Knowledge check

1. True or false: You need to purchase an Azure account before you can use any Azure resources.

    - [X] False

    - [ ] True

2. What is meant by cloud computing?

    - [X] Delivery of computing services over the internet.

    - [ ] Setting up your own datacenter.

    - [ ] Using the internet

3. What is not a reason to move to the cloud?

    - [ ] Faster innovation

    - [X] A limited pool of services

    - [ ] Speech recognition and other cognitive services

# Fundamental Azure concepts

## Intro

Work in the IT department for Tailwind Traders, which has decided to migrate its applications and data to Microsoft Azure.  

Learning objectives:  
- Identify the benefits and considerations of using cloud services.  
- Describe the differences between categories of cloud services.  
- Describe the differences between types of cloud computing.  

## Different cloud models

| Public                                | Private                                           | Hybrid                            |
|  ---                                  |   ---                                             |  ---                              |
| over public Internet                | on-premises                                     |  combined                        |
| easily scalable                     | hardware must be purchased                      | more flexible                   |
| quick app provision / deprovision   | complete control over resources and security    | choose where app run            |
| pay-as-you-go                       | maintenance hardware and security               | control security, compliance    |

## Cloud benefits

1. Advantages
    - High availability  
    - Scalabitily  
    - Eslaticity  
    - Agility  
    - Geo-distribution  
    - Disaster recovery  

2. Expenses

    - Capital Expenditure (CapEx): up-front cost for physical infra for example  

    - Operational Expenditure (OpEx): expense for services or products and deductable now - Consumption-based model

Cloud computing is a consumption-based model

## Categories of cloud services

![alt text](../images/iaas-paas-saas.png "Cloud services illustration")

|                                        | Short description            | Advantages    | Disadvantages
| ---                                    | ---                          | ---           | ---
| **Infrastructure-as-a-Service (IaaS)** | Renting hardware             | - No CapEx<br>- Agility<br>- No strong skills<br>- Consumption-based model<br> | 
| **Platform-as-a-Service (PaaS)**       | Managed hosting platform     | - No CapEx<br>- Agility<br>- No strong skills<br>- Consumption-based model<br>- Users can focus on app dev only | Platform limitations
| **Software-as-a-Service (SaaS)**       | Managed software             | - No CapEx<br>- Agility<br>- No strong skills<br>- Pay-as-you-go pricing model<br>- Users can focus on app dev only | Software feature limitatitons

![alt text](../images/cloud-model-shared-responsibility.png "Cloud service model")

*Serverless computing* is like PaaS which manages the infrastructure required to run the application code.  

## Knowledge check

Choose the best response for each question. Then select Check your answers.

1. Which of the following choices isn't a cloud computing category?  
    - [X] Networking-as-a-Service (NaaS)  
    - [ ] Platform-as-a-Service (PaaS)  
    - [ ] Infrastructure-as-a-Service (IaaS)  
    - [ ] Software-as-a-Service (SaaS)  

2. Which of the following statements is true?  
    - [ ] With Operating Expenses (OpEx), you are responsible for purchasing and maintaining your computing resources.  
    - [X] With Operating Expenses (OpEx), you are only responsible for the computing resources that you use.  
    - [ ] With Capital Expenses (CapEx), you are only responsible for the computing resources that you use.  

3. Which of the following options isn't a type of cloud computing?  
    - [X] Distributed cloud  
    - [ ] Hybrid cloud  
    - [ ] Private cloud  
    - [ ] Public cloud  

4. Which of the following choices isn't a benefit of using cloud services?  
    - [ ] Scalability  
    - [ ] Disaster recovery  
    - [ ] High availability  
    - [X] Geographic isolation  

# Azure architecture fundamentals

## Overview

Four levels in Azure:  

- management groups: manage access, policy and compliance for multiple subscriptions  
- subscriptions: Manage costs and the resources created by users, teams or projects  
- resources groups: logical container into which resources are  
- resources: created instances of services  

![alt text](../images/resources-level.png "Resources levels in Azure")

## Regions availability zones  

`Region` is a geographical area that contains at least one but potentially multiple datacenters that are nearby and networked together with a low-latency network.  
Examples: West US, West Europe, Australia East, ...  

### Special Azure regions

Exist for compliance or legal purposes  
Examples: US DoD Central, US Gov Virginia, China East  

### Availability zone

Physically separate datacenters within an Azure region.
It is set up to be an isolation boundary.  

![alt text](../images/availability-zones.png "Availability zones")
