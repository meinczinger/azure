# Azure monitoring

## Monitoring baselines

"What is normal" in terms of CPU, network etc.

## Azure monitoring and service health

- Azure resoruce activity log
- Azure performance diagnostics Windows WM extension
- Custom dashboards can be created
- Azure application insights can be used for web apps


## Log analytics workspace 

- Centralized monitoring for azure data log
- Feeds into azure monitor
- Log quieries
- Alert notifications


Data sources for log analytics:
- Stroage account logs
- Azure activity logs
- Physical and virtual servers
- System center operations manager (SCOM)

## Individual resource monitoring

E.g. activity log of a VM contains all the management activities of the VM. 

Metrics show CPU, RAM etc. for the VM, custom metrics can be added.

Logs can be enabled on the VM, it outputs the logs into a log analytics workspace.

## Log analytics workspace

It is a resource, which can be created and configured. It is created in a specific location and resource group.

Datasourcec can be then connected to it, e.g. a VM log can be connected.

There is one default analytics workspace created by region.


Data sources:
- VMs
- Storage accounts
- Azure activity logs


## Log queries

Many existing queries exist, which can be used or adjusted. A query can be pinned to a dashboard. 

## Application insights

For web apps, application insights can be enabled.

## Network performance monitor

Within the log analytics workspace, the network performance monitor needs to be added manually.

- OMS agent needs to be installed on the monitored hosts
- Networks to be monitored need to be added to the config
- Same for subnets
- Same for VMs
- Performance monitoring rules can be added, including alerts

## Network watcher

Shows:
- Topology of the network
- A connection between a source and destination VM can be monitored
- Packet capture can be executed
- VPN troubleshoot
- Next hop