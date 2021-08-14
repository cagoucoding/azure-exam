# Azure Monitor  

## Intro  

Collecting, analyzing and acting on telemetry  

## Pillars of Observability  

![alt text](../images/three_pillars_of_observability.png "Three pillars of Observability")  

- Metrics: number that is measured over period of time  

- Logs: text file where each line contains event data  

- Traces: history of request that is travels through multiple apps/services  

## Anatomy of Azure Monitor  

![alt text](../images/azure_monitor_anatomy.png "Architecture of Azure Monitor")  

*sources of data* -> *data stores* -> *functions*  

## Sources (data types)  

- Application code: performance and functionality of application and code    

- Guest OS  

- Azure resources: internal operation of an Azure Resource  

- Azure subscription: service health  

- Azure tenant: operation of tenant-level as AAD  

- Custom  

## Data Stores  

Azure Monitor collects two fundamental type of data from sources:  

- Azure Monitor Logs  
  - collects and organizes logs and perf data  
  - are consolidated into workspaces  
  - works with log queries and the results using **Log Analytics**  

- Azure Monitor Metrics  
  - collects numeric data from monitored resources into a time series database  
  - lightweight and supporting near real-time scenarios (useful for alerting)  
  - can be analyzed using **Metrics Explorer**  

## Log Analytics  

To edit and run log queries with data in Azure Monitor Logs  

### Log Analytics workspaces  

An unique environment for Azure Monitor log data  

### Kusto and Kusto Query Language (KQL)  

Kusto is based on relational databse management systems  

Logs queries are written the KQL  

#### Kusto Entities  

- Clusters  
- Databases  
- Tables  
- Columns  
- Functions  

#### Kusto Scalar Data types  

Scalars are quantities that are fully described by a magnitude (or numerical value)  

Data type defines how a piece of data is interpreted  

#### Kusto Control Commands  

Can modify data and metadata and has it own syntax different from KQL  

Example:  
```
.show tables
| count
```

#### Kusto Functions  

- Stored Functions  

- Query-defined Functions  

- Built-in Functions  

#### Kusto Scalar Operators  

- Bitwise (binary)  

- Logical (binary) 

- Datetime / timespan arithmetic  

- Numerical  

- String  


#### Kusto Tabular Operators  

- `count`: returns the count of rows in the table  

```
StormEvents | count
```

- `take`: returns up to the specified number of rows of data  

```
StormEvents | take 5
```

- `where`: filters a table to the subset of rows that satisfy a predicate  

```
StormEvents 
| where EventType == "Snow"
```

- `sort`: sort the rows  

```
StormEvents 
| where EventType == "Snow"
| sort by Intensity desc
```

- `project`: returns a specific set of columns  

```
StormEvents 
| take 5
| project StartTime, EndTime, State, EventType
```

- `top`  

- `extend`: creates a new column by computing a value    

```
StormEvents 
| where EventType == "Snow"
| sort by Intensity desc
| extend Duration = EndTime - StartTime
| project StartTime, EndTime, State, EventType
```

- `summarize`: aggregates groups of row  

- `render`: renders results as a graphical output  

## Metrics Explorer  

Plot charts, visualize correlating trends and investigate spikes and dips in metrics values  

To visualize a metric you need to define:  

- scope  
- namespace  
- metric  
- aggregation  

## Azure Alerts  

For notifying you when issues are found with your infrastructure or app  

3 types of alerts:  

- Metrics Alerts  
- Log Alerts  
- Activity Logs Alerts  

![alt text](../images/azure_monitor_alerts.svg "Azure Alerts architecture")  

## Azure Dashboards  

Virtual workspaces to quickly launch tasks for day-to-day operations 
and monitor resources  

## Azure Workbooks  

**It tells a story about the performance and availability about your applications 
and services**  

## Application Insights  

Application Performance Management (APM) service  

Use cases:  
- automatically detect perf anomalies  
- includdes powerful analytics tools to help you diagnose issues 
and to understand what users do with your app  
- designed to help you continuously improve perf and usability  
- integrates with your DevOps process  
- can monitor and analyze telemetry from mobile apps  

## Exercises  

> **_TODO_**: Do and document these exercises  

- Knowledge check - [Configure Azure Monitor](https://docs.microsoft.com/en-us/learn/modules/configure-azure-monitor/8-knowledge-check)  

- Knowledge check - [Configure Azure Alerts](https://docs.microsoft.com/en-us/learn/modules/configure-azure-alerts/5-knowledge-check)  

- Knowledge check - [Configure Log Analytics](https://docs.microsoft.com/en-us/learn/modules/configure-log-analytics/8-knowledge-check)  

- Exercise - [Use metric alerts to alert on performance issues in your Azure environment](https://docs.microsoft.com/en-us/learn/modules/incident-response-with-alerting-on-azure/4-exercise-metric-alerts)  

- Exercise - [Use activity log alerts to alert on events within your Azure infrastructure](https://docs.microsoft.com/en-us/learn/modules/incident-response-with-alerting-on-azure/7-exercise-activity-log-alerts)  

- Exercise - [Create basic Azure Monitor log queries to extract information from log data](https://docs.microsoft.com/en-us/learn/modules/analyze-infrastructure-with-azure-monitor-logs/4-exercise-create-log-queries)  

- Exercise - [Set up a Log Analytics workspace and Azure Monitor VM Insights](https://docs.microsoft.com/en-us/learn/modules/monitor-performance-using-azure-monitor-for-vms/3-exercise-set-up-log-analytics-workspace)  

- Exercise - [Build log queries](https://docs.microsoft.com/en-us/learn/modules/monitor-performance-using-azure-monitor-for-vms/5-exercise-build-log-queries)  


# Azure Backup Service  

## Intro  

Directly integrated with Azure Services  

What can I backup:  

- On-Premise  
- Azure VMs  
- Azure Files  
- SQL Server  
- SAP HANNA databases  
- Azure Databases  

## Azure Recovery Service (ARS) Vault  

Storage entity in Azure that houses data and recovery points  

It supports:  
- System Center Data Protection Manager (DPM)  
- Windows Server  
- Azure Backup Server  
- ...

Its features:  
- enhanced capabilities to help secure backup data  
- central monitoring for your hybrid IT environment  
- Azure RBAC  
- soft delete  
- Cross Region Restore  

## Microsoft Azure Recovery Services (MARS) agent 

Can backup files, folders and system state for Windows VMs *only*  

## Backup Policy  

Configure it with:  
- datasource type  
- frequency  
- number of snapshots retained  
- time range for retention  

## Azure Site Recovery (ASR)  

For business continuity and disaster recovery strategy  

## Follow along  

### Create a Recovery Services Vault  

- Create a Backup Vault 

```
Backup center
└ Backup Vault
  ├ Resource group: az104
  ├ Vault name: az104-vault
  ├ Region: France Central
  └ Review+create
```

- Configure the backup vault  

```
Backup center
└ ## select the backup vault ##
  └ Backup
    ├ Backup goal
    ├ Configure Backup
    └ Add
```

## Exercises  

> **_TODO_**: Do and document these exercises  

- Knowledge check - [Configure file and folder backups](https://docs.microsoft.com/en-us/learn/modules/configure-file-folder-backups/7-knowledge-check)  

- Knowledge check - [Configure virtual machine backups](https://docs.microsoft.com/en-us/learn/modules/configure-virtual-machine-backups/11-knowledge-check)  