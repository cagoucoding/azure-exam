# Explore Azure compute services

## Overview of Azure compute services  

It is an on-demand computing service for running cloud-based applications.  
It provides computing resources such as disks, processors, memory, networking, and operating systems.  

Most prominent services are:

- Azure Virtual Machines: software emulations of physical computers, including:  
  - virtual processor  
  - memory  
  - storage  
  - networking  
  - hosting OS  

- Virtual Machine Scale Sets: sets of identitcal VMS designed to support autoscaling (scale up/down).  

- Azure Container Instances/ Kubernetes Services: compute resources that you can use to deploy and manage containers.

- Azure App Service: you can quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform.  

- Azure Functions: ideal when you're concerned only about the code running your service and not the underlying platform or infrastructure.  

## Azure Virtual Machines  

Ideal for:  

- Total control over the operating system (OS).  
- The ability to run custom software.  
- To use custom hosting configurations.  

Examples of use cases:  

- During testing and development  
- When running applications in the cloud  
- When extending your datacenter to the cloud  
- During disaster recovery  

Two possibility to scale VMs in Azure:

- Virtual machine scale sets: group of identical load-balanced VMs. Autoscaling possible.    
- Azure Batch: large-scale parallel and hig-performance computing batch jobs for scaling many VMs.     

## Azure App Service

App Service enables you to build and host web apps, background jobs, mobile back-ends, 
and RESTful APIs in the programming language of your choice without managing infrastructure.  

Types of app services:  

- Web apps: Java, Ruby, Node.js, PHP or Python apps running on Windows or Linux OS.   
- API apps: REST-based web APIs.  
- WebJobs: run a program or script. Often used to run background tasks.  
- Mobile apps  

## Azure Container Instances or Kubernetes Service

- **Azure Container Instances**: simplest way to run a container in Azure.  

- **Azure Kubernetes Service**: complete orchestration service for containers.  

## Azure Functions  