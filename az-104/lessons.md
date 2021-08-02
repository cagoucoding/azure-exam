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

## Manage Resource Groups  

